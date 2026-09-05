## Administration vs Usage

**Administration:**
- COnfigure and set up the platform
Administration has possibilities of high impact security misconfigurations
- Most important part is Access Management, managing user access to resources and services

**Usage:**
- Use the platform for it's actual purpose

In AWS you create IAM(Identity and Access Management) users, groups, roles, and policies to manage access to resources and services.

### Securing AWS Account

- Don't use ROOT user.
- Don't use access keys for the root user
- Configure MFA for all AWS accounts.

**Root User usage:**
- Billing and Cost Management
- Close AWS accounts
- Change account settings

**IAM Users:**
- There are 2 types of access:
    - AWS Management Console: email and password
    - AWS Command Line Interface (CLI): access keys

**IAM Roles:**
- Offers a secure way to grant permissions to entities, without the need for long-term access keys.
- Roles are often used for services or instances that need to access other services within the cloud environment.

**Key aspects of IAM Roles:**
- AWS Identity: similar to a user, AWS Identity with permission policies
- Assumption: entities assume roles when they need to perform certain actions on resources
- No Permanent credentials: temporary credentials are dynamically generated when the role is assumed.