## Kubernetes Security Best Practices

### 1. Image Scanning

**What security issues can be in image building process?**

- Code from untrusted registries
- Vulnerabilities in tools of OS or libraries
- Unnecessary dependencies that have security issues

**How or when to do image scanning:**

- Scanning during build in CI/CD pipeline
- Regularly scan in Container Registry

### 2. Run Container as Non-Root User

- Create a dedicated user and group
- Set required permissions

- Set configs in the Dockerfile and in Kubernetes manifests

### 3. Manage Users and Permissions

Configure **Authentication:** Who can access the cluster and **Authorization:** What permissions do they have.

- Use Role-Based Access Control (RBAC) to define roles and assign them to users or groups.

### 4. Use Network Policies

**Communication Between Pods:**

- By default : Comunication between Pods is unencrypted!
- If an attacker gets access to one Pod, they can access all other Pods!

**Limit the communication with Network Rules**

- Control traffic flow at the IP address or port level:
  - Which pod can talk to which
  - Which pods they can receive traffic from
- You can do that using "NetworkPolicy" resource
- Apply Least Access Allowed Rules
- With Service Mesh you can do that on service level

### 5. Encrypt Communication

**Enable mTLS between Pods**

- All cluster internal communication should be encrypted 
- If an attacker intercepts traffic, it won't be readable

### 6. Secure Secret Data

- Use K8s own solution, enable EncryptionConfiguration resource
- Use 3rd-party secret management solution - use tools like Vault store and manage keys securely

### 7. Secure etcd

**Why it's important?**
- Secret and all other K8s config data are stored in etcd
- Kubernetes backing store for all cluster data

- Put etcd behind a firewall
- Encrypt etcd data

### 8. Backup and Restore

- Have a proper automated backup and restore in place
- Store backup safely

### 9. Configure Security Policies

**Define Policies to enforce specific configurations**
 