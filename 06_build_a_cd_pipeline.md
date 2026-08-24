## Module Overview
In this module we create an AWS ECR repository and 2 AWS EC2 instances. We will then create a CI/CD pipeline that builds a Docker image of the OWASP Juice Shop application and push it to ECR and deploys it to the EC2 instances.
The second EC2 instance will be used as GitLab Runner to run the CI/CD pipeline.
Self hosted GitLab Runner is a tool that allows you to run your CI/CD jobs on your own infrastructure instead of using GitLab's shared runners.

```yaml
build_image:
  stage: build
  image: docker:24
  services:
    - docker:24-dind
  before_script:
    - apk add --no-cache aws-cli
    - apk add --no-cache --upgrade libexpat aws-cli
    - aws ecr get-login-password --region $AWS_DEFAULT_REGION | docker login --username AWS --password-stdin $AWS_ACCOUNT_ID.dkr.ecr.$AWS_DEFAULT_REGION.amazonaws.com
  script:
    - IMAGE_NAME="$AWS_ACCOUNT_ID.dkr.ecr.$AWS_DEFAULT_REGION.amazonaws.com/juice-shop"
    - docker build -t $IMAGE_NAME:$CI_COMMIT_SHA -t $IMAGE_NAME:latest .
    - docker push $IMAGE_NAME:$CI_COMMIT_SHA
    - docker push $IMAGE_NAME:latest

deploy_image:
  stage: deploy
  image: debian:bullseye-slim
  before_script:
    - apt-get update -y && apt install openssh-client -y
    - eval $(ssh-agent -s) # Starts a background SSH Agent process and configures the terminal session to talk to it.
    - chmod 400 "$SSH_PRIVATE_KEY"
    - echo "$SSH_PRIVATE_KEY" | ssh-add - # Loads the SSH private key to the active agent
    - mkdir -p ~/.ssh
    - chmod 700 ~/.ssh
  script:
    - ssh -o StrictHostKeyChecking=no $SERVeR_USER@$SERVER_IP "docker pull $IMAGE_NAME:latest" # By setting -o StrictHostKeyChecking=no you I disable the "Are you sure you want to continue connecting (yes/no)?"
    - ssh -o StrictHostKeyChecking=no $SERVeR_USER@$SERVER_IP "docker stop juice-shop || true && docker rm juice-shop || true" # || true forces the pipeline to ignore the failure error and keeps going in case the commmand before fails
    - ssh -o StrictHostKeyChecking=no $SERVeR_USER@$SERVER_IP  "docker run -d --name juice-shop -p 3000:3000 $IMAGE_NAME:latest"
```

When we creat the EC2 instance for the GitLab runner it needs some higher specs, so we used:
- Instance type: t3.large
- Storage: 20 GB

Once the instance is created, we created the gitlab-runner in Gitlab. The configured the instance with the following command:

```bash
# update package repos
sudo apt update

# Install gitLab runner
curl -L "https://packages.gitlab.com/install/repositories/runner/gitlab-runner/script.deb.sh" | sudo bash
sudo apt install gitlab-runner -y

# Install docker on Ubuntu 22.04
sudo apt  install docker.io -y

# Add gitlab-runner & ubuntu users to docker group
sudo usermod -aG docker gitlab-runner
sudo usermod -aG docker ubuntu

# Install AWS CLI 
sudo apt install awscli -y

# Register runner
sudo gitlab-runner register \
--url "https://gitlab.com/" \
--token "registration-token-here" \
--executor "shell"
```