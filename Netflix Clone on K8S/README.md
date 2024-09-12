**DEPLOY NETFLIX CLONE ON K8S**

![devsecops_netflix](https://github.com/user-attachments/assets/05a3e5e0-a1c0-4397-9825-182e6a2835eb)

This project seeks to deploy a cloned version of Netflix on a Kubernetes server for access. It employs DevSecOps practices, and uses different tools to this cause.

It is grouped into 3 major phases - DEV, SEC, OPS.

**(A) DEV - Local Development**

1. Create a T2 Large EC2 instance - to accommodate Jenkins, SonarQube, Trivy, especially for the many plugins to be installed on Jenkins.

- About 25 GB of storage.

- Enable HTTP, HTTPS,

- Create an elastic IP for longer use of IP, and associate with your instance.

2. Connect to your EC2 instance on your terminal.

3. Clone git files if stored on your GitHub Repository.

4. Access Docker file and build docker file to get Docker image - docker build

5. Run Docker image to get Docker container - docker run

**TMDB - The Movie Database - used in the Docker file to get the API to fetch movies and series into the app.

7. Open a TMDB account, and generate an API key.

8. Add ports '8081' for app, and '9080' for Jenkins, and '9000' for SonarQube on the inbound rules.

9. Recreate Docker image and container with the generated TMDB API key.

10. App can be accessible locally - http://PublicIP:8081


 **(B) SEC - Security Practices**

 1. Install SonarQube and Trivy on your terminal

SonarQube - Quality Assurance Tool.

Trivy - Open-source security scanner tool for files.

2. Login to SonarQube and change password - http://PublicIP:9000

3. Install Java and Jenkins on your terminal.

4. Login to Jenkins - http://PublicIP:8080 and install recommended plugins.

5. Install additional Plugins - nodejs, eclipse temurin, SonarQube Scanner, OWASP, Docker, Docker Commons, Docker Pipeline, Docker API, Docker-build-step.

6. On Jenkins' UI, set tools for jdk17 and node16.

7. On SonarQube's UI, create token and add token as credential on Jenkins.

8. Search for SonarQube servers on Jenkins, add the token to it.

9. On tools on Jenkins, search for SonarQube scanner and add the installation.

10. Add DockerHub credentials on Jenkins.

11. Create new Pipeline on Jenkins - paste prepared code, type in there, or use Groovy editor.

12. Run Pipeline - project pushes to DockerHub as an image.

13. Run SonarQube Analysis having created a new project and linked it.

**For Docker login failed errors:
_sudo usermod -aG docker jenkins
sudo systemctl restart jenkins_

**(C) OPS - Montoring + Deployment**

MONITORING

1. Create a T2 Medium EC2 instance for Prometheus server.

- 20 GB of space.

- Create elastic IP, and associate with instance.

2. Install Prometheus on your instance on your terminal.

3. Set ownership for Prometheus.

4. Create config file for Prometheus - Prometheus.yaml file.

5. Enable and start Prometheus.

6. Install Node-exporter

- Used on Prometheus to gather system metrics.

7. Enable and start Node-exporter

8. Open ports on instance for Prometheus - '9090' and Node-exporter - '9100'

9. Edit Prometheus.yaml file with configurations for Node-exporter.

10. Install Grafana.

11. Enable and start Grafana.

12. Add port - '3000' on the security group settings.

13. Open Grafana on web and login.

14. Add Prometheus' URL on Grafana's data source.

15. Import dashboard on Grafana - load Node-exporter's dashboard and Prometheus source.

16. Install Prometheus metrics plugin on Jenkins

17. Add Jenkins configurations to Prometheus.yaml file

18. Set up email notifications

- Gmail - App Password Settings - Generate and copy code.

- Jenkins - Manage Jenkins - System - Email - add smtp.gmail.com, add your email address - for smtp authentication, add your gmail account and the code generated. Port is '465'

DEPLOYMENT - ArgoCD, Helm, K8s

1. Create a K8S cluste on AWS - AWS EKS.

2. Create an IAM Node Role

3. Create a node group.

4. Install Helm on your instance.

5. Install Node-exporter using Helm.

6. Install ArgoCD - follow AWS documentation.

7. Expose ArgoCD's server - echo address, and sign in to UI.

8. Add your repository link to ArgoCD UI.

9. Create new app on ArgoCD.

10. Add the app's port as shown on the Node group's security group settings + the node-exporter's port in there as well.

11. Add the Node-exporter metrics path on your Prometheus.yaml file.

12. Finally, launch cloned Netflix app on your browser with the public IP of the node-group and the port number as found on the app.
