# Authorization with Cloud IAM

## Introduction
Cloud Identity and Access Management (IAM) enables you to manage access control by defining who (the principal) has what access (role) to which resource. By following the principle of least privilege, you ensure that users and services have only the permissions they need to perform their tasks.

## Key Concepts in IAM

### Principals
Principals are entities that can be granted access to resources. There are several types of IAM principals:

1. **Google Account**:
   - Represents an individual user, such as a developer or administrator.
   
2. **Service Account**:
   - Represents an application or compute workload, rather than an individual user.
   - Allows running code on Google Cloud with specific permissions.

3. **Google Group**:
   - A named collection of Google Accounts and service accounts.
   - Has a unique email address and allows batch management of access controls.
   - Cannot be used to establish identity for resource requests.

4. **Google Workspace Account**:
   - Represents a virtual group of all Google Accounts within an organization.
   - Associated with the organization’s domain (e.g., example.com).
   - Facilitates convenient permission management but cannot establish identity.

5. **Cloud Identity Domain**:
   - Similar to Google Workspace Account, representing a virtual group of all Google Accounts in an organization.
   - Users do not have access to Google Workspace applications.
   - Cannot establish identity but useful for managing access policies.

### Resources
Resources are the Google Cloud entities to which you can grant access. Examples include:
- Projects
- Compute Engine instances
- Cloud Storage buckets
- Artifact Registry repositories

### Permissions and Roles
Permissions specify the operations allowed on a resource, such as `pubsub.subscriptions.consume`. Permissions are grouped into roles, which can be assigned to users.

#### Types of Roles:
1. **Basic Roles**:
   - Highly permissive and broad access.
   - Example: `Viewer` role with read-only access to all resources in a project.
   - Not recommended for production environments due to their broad access.

2. **Predefined Roles**:
   - Provide granular access to specific Google Cloud resources.
   - Created and maintained by Google.
   - Example: `run.invoker` role, which allows invoking Cloud Run services.

3. **Custom Roles**:
   - User-defined roles for specific needs when predefined roles are too permissive.
   - Allow enforcing the principle of least privilege.
   - You have full control over the permissions included in the role.

## Principle of Least Privilege
- **Definition**: Grant each principal only the permissions necessary for their tasks.
- **Implementation**: Use predefined and custom roles to ensure principals do not have more access than needed.

## Example Scenario
- All users in a Google Group named "staff" are granted the `InstanceAdmin` role on `project_a`.
- Each user inherits all permissions contained in the `InstanceAdmin` role.

## Managing Access
- **Granting Access**: Assign roles to users, groups, or service accounts to grant permissions.
- **Changing Access**: Modify roles or permissions as needed to adapt to changing requirements.

## Conclusion
Cloud IAM provides a flexible and secure way to manage access to Google Cloud resources. By understanding principals, resources, permissions, and roles, you can effectively control who has access to what, ensuring security and compliance in your cloud environment.