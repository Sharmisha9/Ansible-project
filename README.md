UPSF Project with Ansible and Nginx  -   upsf.psharmisha.com/data1=data/philadelphia,yelp,none

Overview
This document provides a comprehensive guide on deploying the UPSF project, leveraging Ansible and Nginx within a Linux environment. The UPSF project is built using Angular (with D3.js for data visualization), Node.js for backend operations, and incorporates techniques from text mining and computational topology.

Initial Setup
Ansible Installation
The deployment process begins with the installation of Ansible on a Linux machine. Ansible facilitates the automation of deployment and configuration processes, allowing for efficient and replicable setups.

Virtual Machine and SSH Configuration
A virtual machine (VM) hosted on Oracle Cloud serves as the target for deployment. To securely connect to this VM, an SSH key is generated on the Ansible controller (our local machine), and this key is used to establish a secure connection to the VM. The IP address and SSH key of the VM are crucial for this step.

Repository and Inventory Setup
An essential part of the setup involves creating a Git repository to store all Ansible files, including playbooks. This approach enables collaborative work on the deployment scripts. Additionally, an inventory file is created to list the hosts involved in the deployment process, categorizing them into a controller node (our local machine) and a managed node (the Oracle Cloud VM).

Configuration Files
The ansible.cfg file is created to instruct Ansible on default behaviors, including which inventory file to use. This configuration ensures Ansible operates consistently with our predefined settings.

Nginx Configuration
Upon setting up the Ansible environment, Nginx is installed on the local machine. By default, Nginx listens on port 80. The Nginx configuration file is customized with specific contexts and directives to serve the UPSF project. The root directive is particularly important, as it specifies the path to the dist folder containing the project's static and data files. This setup ensures that when port 80 is accessed, the content served is from the specified dist folder.

Automation with Ansible
To avoid manual SSH and file transfer processes to the Oracle Cloud server, an Ansible playbook is created. This playbook contains tasks and handlers that automate the transfer of the project folder and the Nginx configuration file to the Oracle Cloud VM. The playbook execution is triggered with the command ansible-playbook --ask-become-pass <playbook_file.yml>, facilitating the movement of necessary files to the remote server.

Server Configuration and DNS Setup
Upon successful transfer of files, the Oracle Cloud VM's firewall settings are adjusted to allow traffic through all ports, making the application accessible over the internet. A DNS record is created to map a user-friendly domain name (e.g., www.example.com) to the VM's IP address, improving accessibility. Additionally, a subdomain from AWS and an SSL certificate are employed to secure connections to the server, ensuring encrypted communication.

Conclusion
This document outlines the steps required to deploy the UPSF project using Ansible for automation and Nginx as a web server. By following this guide, the application is made accessible over the internet, hosted securely on an Oracle Cloud VM, with a user-friendly domain and SSL encryption.
