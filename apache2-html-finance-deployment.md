# Apache2 Setup and HTML Template Deployment on Ubuntu

This document presents my personal project to set up an Apache2 web server on Ubuntu using Vagrant and deploy an HTML template for a mock finance site. The goal was to gain hands-on experience with virtual machine configuration, web server setup, and file deployment in a Linux environment.

## Project Overview

I used Vagrant to initialize and configure a virtual machine, set up Apache2 to serve web content, and deployed a downloadable HTML template. This project helped me understand the steps involved in configuring a server and deploying a static website, providing a foundation for future server and web development projects.

## Steps

1. Create Project Folder:
   - Created a folder named `C:\vagrant-vms`.

2. Navigate and Create Directory:
   - Navigated to the folder and created a directory in Git Bash:
     ```bash
     cd C:\vagrant-vms
     mkdir finance
     cd finance
     ```

3. Initialize Vagrant:
   - Ran the following command to initialize Vagrant with the `ubuntu/focal64` box:
     ```bash
     vagrant init ubuntu/focal64
     ```

4. Edit Vagrantfile:
   - Opened the `Vagrantfile` for configuration:
     ```bash
     vim Vagrantfile
     ```
   - Made the following changes in insert mode:
     - Uncommented the private IP address line and set it to `192.168.56.22` (ensuring it doesn’t conflict with other IPs).
     - Uncommented the `config.vm.provider "virtualbox" do |vb|` line.
     - Uncommented the `vb.memory` line (kept the default memory but noted it can be increased if needed).
   - Saved and exited the editor with `Esc`, `:wq`.

5. Start the Virtual Machine:
   - Brought up the VM with:
     ```bash
     vagrant up
     ```

6. Log into the VM:
   - Logged into the VM:
     ```bash
     vagrant ssh
     ```

7. Switch to Root User:
   - Switched to the root user:
     ```bash
     sudo -i
     ```

8. Change Hostname:
   - Edited `/etc/hostname` to set the hostname as `finance`:
     ```bash
     vi /etc/hostname
     ```
   - Saved and exited (`Esc`, `:wq`), then ran:
     ```bash
     hostname finance
     ```
   - Logged out and logged back in:
     ```bash
     exit
     vagrant ssh
     ```

9. Install Required Packages:
   - Installed Apache2, wget, vim, zip, and unzip:
     ```bash
     sudo apt install apache2 wget vim unzip zip -y
     ```

10. Start and Enable Apache2:
    - Started the Apache2 service:
      ```bash
      systemctl start apache2
      ```
    - Enabled Apache2 to start on boot:
      ```bash
      systemctl enable apache2
      ```

11. Verify IP Address:
    - Ran the following to check the IP address:
      ```bash
      ip addr show
      ```
    - Copied the IP and checked it in a browser to ensure Apache2 was running correctly.

12. Verify Web Root Directory:
    - Navigated to the Apache2 web root directory:
      ```bash
      cd /var/www/html/
      ```
    - Listed the contents to verify the directory where Apache serves files:
      ```bash
      ls
      ```

13. Download HTML Template:
    - In a browser, visited [Tooplate.com](https://www.tooplate.com/) and selected the "Mini Finance" template. Copied the direct download link using the Developer Tools (F12) and went to the Network tab.

14. Download and Unzip Template:
    - Changed directory to `/tmp` and downloaded the template:
      ```bash
      cd /tmp/
      wget https://www.tooplate.com/zip-templates/2135_mini_finance.zip
      ```
    - Unzipped the downloaded file:
      ```bash
      unzip 2135_mini_finance.zip
      ```
    - Navigated into the extracted directory:
      ```bash
      cd 2135_mini_finance
      ls
      ```

15. Copy Files to Web Root:
    - Copied all files from the template folder to the Apache2 web root:
      ```bash
      cp -r * /var/www/html/
      ```

16. Restart Apache2 Service:
    - Restarted the Apache2 service to apply changes:
      ```bash
      systemctl restart apache2
      ```

17. Check Apache2 and Firewall Status:
    - Checked Apache2 status:
      ```bash
      systemctl status apache2
      ```
    - Verified firewall status:
      ```bash
      systemctl status firewalld
      ```
    - Stopped and disabled the firewall (note: not recommended for production):
      ```bash
      systemctl stop firewalld
      systemctl disable firewalld
      ```

18. Access Deployed Template:
    - Retrieved the IP address with:
      ```bash
      ip addr show
      ```
    - Opened the IP in a browser to view the deployed HTML template.


