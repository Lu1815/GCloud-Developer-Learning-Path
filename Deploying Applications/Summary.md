# Summary: Continuous Integration and Delivery, and Containerization

## Continuous Integration and Delivery (CI/CD)
- **Purpose**: Provides a stable, repeatable process for building and deploying applications.
- **Continuous Integration**: Developers commit changes to a code repository, triggering automatic builds.
  - **Build Service**: Tools like Cloud Build generate application containers and executables.
  - **Artifact Storage**: Artifacts are stored in a repository such as Artifact Registry.
- **Continuous Delivery**: Changes pushed to the main branch trigger builds and deployments.
  - **Deployment System**: Deploys application images to environments like Cloud Run or GKE.
  - **Testing**: Integration and performance tests are run in staging environments.
  - **Release Candidate**: Successful builds are tagged for potential release, requiring manual approval for production deployment.

## Building and Maintaining Container Images
- **Containers**: Lightweight and portable, providing efficient packaging and deployment of applications.
  - **Separation of Responsibilities**: Developers handle application logic and dependencies; IT operations manage deployment.
  - **Workload Portability**: Containers can run anywhere, simplifying promotion across development, test, and production environments.
  - **Application Isolation**: Containers provide isolated environments, allowing different dependencies without conflicts.

### Cloud Build
- **Service Overview**: A fully managed service for setting up build pipelines.
- **Key Features**:
  - Automatically triggered builds on code commits.
  - Creates Docker container images and pushes them to Artifact Registry.
  - No need to download build tools or manage infrastructure.

### Setting Up a Build Pipeline
- **Build Triggers**: Configured based on commits to specific branches or tags.
- **Build Configuration File**: Specifies build steps, written in YAML or JSON.
  - **Steps**: Each step is a Docker container invoked by Cloud Build.
  - **Source Code Mounting**: Mounted into the `/workspace` directory of the Docker container.
  - **Artifact Persistence**: Artifacts produced are stored in the `/workspace` folder for use in subsequent steps.
- **Artifact Registry**: Manages and secures build artifacts, providing vulnerability scanning and continuous monitoring.

### Additional Features
- **Binary Authorization**: Ensures only trusted container images are deployed to production.
- **Security Insights**: Integrated with GKE and Cloud Run for continuous security assessments and recommendations.

## Conclusion
This module covered the essentials of CI/CD and containerization:
- **CI/CD**: Establishes a reliable process for building and deploying applications.
- **Containerization**: Provides an efficient method for packaging applications, with benefits such as separation of responsibilities, workload portability, and application isolation.
- **Google Cloud Tools**: Cloud Build and Artifact Registry simplify the creation and management of container images, enhancing security and efficiency in the CI/CD pipeline.