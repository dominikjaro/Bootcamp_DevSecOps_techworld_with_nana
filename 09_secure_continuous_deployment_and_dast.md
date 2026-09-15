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
