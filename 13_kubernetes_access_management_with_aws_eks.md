## K8s Authentication and Authorization

**Authentication**

- API server handles authentication of all the requests
- Available authentication strategies:
  - Client Certificate
  - Statis Token File
  - 3rd Party Identity Service, like LDAP

A csv file with a minimum of 3 columns: token, user name, user uid, followed by the group names

**Authorization**

The best practice is to use the Least Privilige Rule and grant Admin Access and Limited Access.

- Admin Access: need cluster-wide access to do tasks like configure namespaces etc.
- Limited Access: developers need only limited access, for example to deploy application to 1 specific namespace

### RBAC (Role-based Access Control)

- Enable RBAC: `kube-apiserver --authorization-mode=RBAC --other-options`
- 4 kinds of K8s resources: ClusterRole, ClusterRoleBinding, Role, RoleBinding

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  namespace: default
  name: pod-reader
rules:
- apiGroups: [""]
  resources: ["pods"]
  verbs: ["get", "watch", "list"]
```

## AWS IAM Role

- An IAM role is similar to an IAM user, but it is intended to be assumable by anyone who needs it, rather than being associated with a single individual.

**Security benefits:**

- Roles are temporary assumes
- Short-lived credentials reduce the risk of long-term exposure

### AWS and K8s Users and Roles

1. Define Access on AWS Level
   - Give access to EKS cluster with Read-Only permissions using IAM Roles.
   - Rest is handled with K8s RBAC
2. Define K8s Access with RBAC
   - Define Role and ClusterRole based on who you want to give access to what resources in the K8s cluster
3. Create Mapping between IAM Role and K8s User
   - K8s user is bound to a K8s Role with certain permissions

For example:

- **For Administrator:** Grant Read-only permissions on AWS level and ClusterRole read-only permissions on K8s level
- **For Developer:** Grant Read-only permissions on AWS level and read-only Role limiting to a single namespace on K8s level

**NOTE:** In DevOps everything should happen in an **automated way via CI/CD pipelines** So even administrator, should not need to change anything manually. Every change should go through Git (GitOps)

### Mapping from AWS to Kubernetes

**What is "aws-auth" ConfigMap?**

- The aws-auth COnfifMap is automatically created and applied to your cluster when you create a managed node group or when you create a node group using eksctl.
- It is initially created to allow nodes to joint the cluster
- You also use this ConfigMap to add role-based access control RBAC access to IAM principals
- Each entry maps an IAM role to a username and set of groups