## SSM - AWS System Manager

- It's a management service that helps you manage and automate operational tasks across your AWS resources
- `aws ssm` sub command is used to interact with AWS SSM
- Secure end-to-end solution that enables secure operations at scale

- **SSM Agent** runs on EC2 instances

#### Requirements:
- Have SSM Agent installed on EC2 instance
- Attach SSM Role to EC2 Instance. So EC2 instance is allowed to be managed by SSM
  - Machines managed by SSM are called "Nodes"
  - A "managed node" is any machine configured for use with SSM

## GCP - VM Manager (OS Config)

- It's a suite of tools that helps you manage, automate, and apply operational configurations across your GCP virtual machines.
- `gcloud compute os-config` sub command is used to interact with VM Manager (OS Config)
- OS Config Agent runs on GCP virtual machines
#### Requirements:
- Have OS Config Agent installed on GCP virtual machine
- Enable the OS Config API for your GCP project
- Attach Service Account to the VM with the necessary IAM roles like (roles/osconfig.instanceDelegate)

GCP separates specific features into IAP & OS Login.

---
## Security Measures and Continuous Security Imrpovements

1. Created AWS roles for the EC2 instances `gitlab-runner server` AND the `app-server` (permissions: `SSMFullAccess, ContainerRegistryFullAccess, SSMManagedInstanceCore`)
2. Installed and configured SSM Agent on all EC2 instances to enable management through AWS Systems Manager.
   1. to confirm run `sudo systemctl status snap.amazon-ssm-agent.amazon-ssm-agent.service`
3. Removed unnecessary variables (as we don't use ssh anymore)
4. Removed the GitLab user in AWS

## Dynamic Application Security Testing (DAST)

- No knowledge of the internal code or design of application
- Testing based on inputs and outputs, simulating real-world interactions
- We are interacting with app's UI like every other user

- **NOTE:** DAST tests are executed in one of the pre-production environments and if crictical security issues are found the CI/CD pipeline is aborted

### ZAP: BaseLine VS Full Scan

**Baseline:**
- Quick and lightweight - aiming to provide a rapid overview of vulnerabilities without conducting an exhaustive analysis

**Full Scan:**
- Scripts performs actual attacks
- In-depth analysis, including unique attack scenarios
- Take much longer
- Deploy it on its own dedicated environment - at a specific schedule time

