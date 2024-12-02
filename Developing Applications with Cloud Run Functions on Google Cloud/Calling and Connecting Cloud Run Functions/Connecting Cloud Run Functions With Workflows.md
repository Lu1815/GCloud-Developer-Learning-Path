# Study Notes: Connecting Cloud Run Functions with Workflows and VPC Networks

## Workflows Overview

### What is Workflows?
Workflows is a **fully-managed, serverless orchestration platform** provided by Google Cloud. It acts as a central orchestrator for linking and executing a series of services in a specific order, known as a workflow.

### Key Features:
1. **Service Orchestration**:
   - Combines Google Cloud services, Cloud Run functions, and external APIs.
   - Enables building stateful, automated processes.

2. **Observability**:
   - Logs every workflow execution, providing visibility into the current state and making troubleshooting easier.

3. **Flexibility**:
   - Supports long-running processes (up to one year).
   - Can manage state, retry operations, poll, and wait for events.

4. **Centralized Control**:
   - Provides a single source-of-truth for the application flow, ensuring consistency and easier maintenance.

### Use Cases:
- Orchestrating Cloud Run functions, HTTP services, and external APIs.
- Building serverless applications with complex dependencies and state management.

---

## Steps to Build a Workflow

### Step 1: Enable Required APIs
Enable APIs for:
- Cloud Run functions.
- Cloud Run.
- Workflows.
- Any additional services you plan to integrate.

### Step 2: Prepare Functions
1. **Write and Deploy Functions**:
   - Use HTTP functions with HTTP triggers to create endpoint URLs.
2. **Test Functions Individually**:
   - Test using tools like `curl` or other HTTP clients.
   - Test locally before deploying for faster iteration.

### Step 3: Create the Workflow
1. **Workflow Definition**:
   - A workflow is described using steps written in YAML or JSON format.
   - Each step corresponds to a specific action, such as invoking a Cloud Run function or calling an API.
2. **Define Function Connections**:
   - Use HTTP methods (e.g., `GET`, `POST`) to call Cloud Run function endpoints.
   - Pass results from one function as input to the next.

### Step 4: Deploy and Execute the Workflow
Once the workflow is defined and tested, deploy it to Google Cloud and monitor executions through the console.

---

## Workflow Example

### Workflow Steps:
1. **Invoke Cloud Run Functions**:
   - Call two functions (`cfn1` and `cfn2`) using `GET` and `POST` methods.
   - Pass results from `cfn1` as input to `cfn2`.
2. **Call External API**:
   - Connect to an external REST API and pass data from `cfn2` as query parameters.
3. **Integrate Cloud Run Services**:
   - Call a Cloud Run service within the workflow.
   - Use the service’s output as the final result of the workflow.

---

## Connecting Cloud Run Functions to VPC Networks

### Virtual Private Cloud (VPC) Overview
A **VPC network** is a virtual version of a physical network, implemented inside Google’s production infrastructure. It provides:
- **Global Scope**:
  - Consists of regional virtual subnets connected by Google’s global wide area network.
- **Private Communication**:
  - Allows secure communication between resources using internal IP addresses.

---

### Serverless VPC Access
Serverless VPC Access enables Cloud Run functions to securely connect to VPC networks. This is essential for accessing resources with internal IPs, such as:
- Compute Engine instances.
- Memorystore.
- Other private services within the VPC.

#### Benefits:
1. **Secure Communication**:
   - Uses internal DNS and IPs, avoiding exposure to the internet.
2. **Direct Access**:
   - Facilitates seamless integration with private cloud resources.

---

### Steps to Configure Serverless VPC Access

1. **Enable the Serverless VPC Access API**:
   - Activate the API in your Google Cloud project.

2. **Create a Serverless VPC Access Connector**:
   - A connector acts as a bridge between the serverless environment and the VPC network.
   - Assign the connector to:
     - A specific **VPC network**.
     - A **region** (must match the Cloud Run function’s region).
     - A **subnet or CIDR range** configured exclusively for the connector.

3. **Attach Connector to Cloud Run Functions**:
   - Configure each function to use the connector:
     - Use the Google Cloud Console or `gcloud` CLI.
   - Define firewall rules to restrict connector access to specific resources.

4. **Shared VPC Networks**:
   - Functions can also connect to shared VPC resources using connectors.

---

## Additional Resources
For more details, refer to:
- The **Serverless VPC Access documentation**.
- Google Cloud’s official documentation for Cloud Run functions and workflows.

---

## Summary
- **Workflows** orchestrate Cloud Run functions, external APIs, and Google Cloud services into cohesive processes, offering state management, observability, and flexibility.
- **Serverless VPC Access** connects Cloud Run functions to VPC networks, ensuring secure communication with private resources while avoiding public exposure.
- Combining workflows with VPC access enables the creation of robust, secure, and serverless applications that integrate multiple services seamlessly.
