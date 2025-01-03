# Automated Docker Deployment with Jenkins and Ansible

## Overview
This project automates the deployment of a Docker container on a remote virtual machine (VM) using a Jenkins pipeline and Ansible. The pipeline pulls code from GitHub, builds and pushes a Docker image to Docker Hub, and then uses Ansible to install Docker and deploy the container on the target VM.

---

## Architecture

- **Master VM**:
  - Hosts Jenkins.
  - Executes Ansible playbooks.
  - Pushes Docker images to Docker Hub.

- **Slave VM**:
  - Receives Docker installation and container deployment commands from Ansible.
  - Runs the deployed Docker container.

---

## Key Components

### Jenkins Pipeline
The pipeline performs the following steps:

1. **Git Clone**:
   - Clones the project repository from GitHub using saved credentials.

2. **Docker Login**:
   - Logs into Docker Hub using credentials stored in Jenkins.

3. **Run SSH Command**:
   - Tests SSH connectivity to the Slave VM.

4. **Build Docker Image**:
   - Builds a Docker image using the Dockerfile from the cloned repository.

5. **Push Docker Image**:
   - Pushes the built image to Docker Hub.

6. **Run Ansible Playbook**:
   - Executes an Ansible playbook to:
     - Install Docker on the Slave VM.
     - Update packages.
     - Pull and run the Docker container.




### Ansible Playbook
- Installs Docker.
- Updates packages.
- Pulls the Docker image from Docker Hub.
- Runs the container.







---

## Steps to Run

1. Set Up SSH**:
   - Ensure SSH keys are configured for passwordless access from the Master to the Slave VM.

2. Configure Jenkins**:
   - Add credentials for GitHub and Docker Hub.
   - Set up the pipeline using the `Jenkinsfile`.

3. Run the Pipeline**:
   - Trigger the pipeline and monitor its execution in Jenkins.

4. Verify Deployment**:
   - Check the Slave VM to confirm the Docker container is running:
     ```bash
     docker ps
     ```

---

## Troubleshooting

- Permission Issues**: Ensure the `deployer` user has sufficient privileges.
- SSH Failures**: Verify SSH configuration and key access.
- Ansible Errors**: Debug playbook execution using `-vvv` flag.

---

## Conclusion
This project simplifies the process of deploying Docker containers using Jenkins and Ansible, providing a robust CI/CD workflow that can be extended to larger-scale deployments.

                                               Jenkins Pipeline Execution


![diagram-export-12-23-2024-4_10_00-PM](https://github.com/user-attachments/assets/dfea2db3-3e8e-4fcc-b2c6-93297adcbd44)




                                               



![Screenshot 2024-12-23 071507](https://github.com/user-attachments/assets/ce3fce65-0868-4401-8418-d64f6e9d9456)





![Screenshot 2024-12-23 071649](https://github.com/user-attachments/assets/01e5a3b0-d58e-4357-8cd7-08625f7f71c2)






![app](https://github.com/user-attachments/assets/4448f0d8-8d61-4486-b8f6-fcb9bb6d7d0c)

