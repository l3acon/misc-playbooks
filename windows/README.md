# warning
stolen from https://web.archive.org/web/20210618210105/http://blog.hortonew.com/ansible-splunk-forwarder-deployment
Ansible - Splunk Forwarder Deployment - Pt.1
This post will help you get up and running with Ansible with the end goal of deploying Splunk universal forwarders to both Windows and Linux.

# Inspiration
https://github.com/divious1

.conf 2015 talk - Splunk Configuration Management and Deployment with Ansible - Jose Hernandez / Sean Delaney

## Prerequisites
Ansible

Follow installation guidelines here:

http://docs.ansible.com/ansible/intro_installation.html

Install dependencies for connecting to windows hosts

http://docs.ansible.com/ansible/intro_windows.html

Linux Specific

User who can ssh
User who can sudo
Windows Specific

Domain account who can access server via winrm, and install software
A share location that your servers can pull down files from (using your domain account)
HTTP/AllowUnencrypted=True

winrm set winrm/config/service ‘@{AllowUnencrypted=“true”}’

or

HTTPS/AllowUnencrypted=False
# Install Environment
## File Structure
```
/etc/ansible/
 ansible.cfg  (ansible specific settings)
 hosts  (where you can store groups of hosts for ease of management)
 group_vars/
   windows.yml
 playbooks/  (where you should store .yml playbooks)
   SplunkUniversalForwarderInstallWindows.yml
   SplunkUniversalForwarderInstallLinux.yml

   splunk_binaries/  (where you should store installers)
     splunkforwarder-6.3.0-aa7d4b1ccb80-x64-release.msi
     splunkforwarder-6.3.0-aa7d4b1ccb80-linux-2.6-x86_64.rpm

  roles/  (where you can group tasks by Linux/Windows)
    universal_forwarder_linux/
      tasks/
        main.yml
        forwarder.yml
    universal_forwarder_windows/
      files/
        install-splunk.ps1
      tasks/
        main.yml
        forwarder.yml
```
