## GitOps - DevOps for IaC

Takes best practices for application development, such as version control, collaboration and CI/CD and applies them to infrastructure.

### Version Control with Git

- Git naturally becomes part of IaC
- IaC code can be versioned, just like application code
- Enables you to track changes, roll back to previous configurations if needed

### CI/CD for IaC

- Automate deployment and testing of IaC code changes

In the below pipeline we are using Artifacts to persist important files between different stages of the CI/CD process.

**Artifacts VS Cache:**

- **Artifacts:** Used to persist important files between different stages of the CI/CD process. They are uploaded after a job finishes and can be downloaded by subsequent jobs.
- **Cache:** Used to speed up jobs by reusing files from previous runs, such as dependencies or build outputs. Caches are not guaranteed to be preserved and are primarily for performance optimization.

```yaml
variables:
  TF_VAR_env_prefix: "dev"
  TF_VAR_runner_registration_token: $RUNNER_TOKEN
  TF_DIR: "terraform/aws" 

stages:
  - init
  - test
  - build
  - deploy
  - plan-destroy
  - destroy


image:
  name: hashicorp/terraform:latest
  entrypoint: [""]

before_script:
 - cd $TF_DIR

init:
  stage: init
  script:
    - terraform init --upgrade
  artifacts:
    paths:
      - $TF_DIR/.terraform/
      - $TF_DIR/.terraform.lock.hcl

validate:
  stage: test
  script:
    - terraform validate
  allow_failure: true

trivy:
  stage: test
  image:
    name: aquasec/trivy:latest
    entrypoint: [""]
  script:
    - trivy config --format json . > trivy.json
    - trivy config --exit-code 1 --severity HIGH,CRITICAL .
  allow_failure: true
  artifacts:
    when: always
    paths:
      - $TF_DIR/trivy.json

build:
  stage: build
  script:
    - terraform plan -out "planfile"
  artifacts:
    paths:
      - $TF_DIR/planfile

deploy:
  stage: deploy
  script:
    - terraform apply --input=false "planfile"
  when: manual

### DESTROY STAGE ###
plan-destroy:
  stage: plan-destroy
  needs: ["init"]
  script:
    - terraform plan -destroy -out "destroyplan"
  when: manual
  artifacts:
    paths:
      - $TF_DIR/destroyplan

destroy:
  stage: destroy
  needs: ["plan-destroy"]
  script:
    - terraform destroy --input=false "destroyplan"
  when: manual
  ```

---

## Terraform state

- TF must store state about your managed infrastructure and configuration
- This state is used by TF to map real world resources to the configuration

### Best Practice - Configure Remote State

- Central storage for IaC
- Remote store, like S3 bucket, instead of a local state and local filesystem

### Automated Terraform Security Scan

`terraform validate` command checks for syntax validity, general correctness of attributes, variables, modules

**Using trivy:** scans TF for security vulnerabilities in infra configuration (static analysis)

