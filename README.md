## AWS JBoss Deployment
Spin up an aws instance, install jboss, and deploy an app

This playbook was designed for Ansible Tower demo purposes and is in part adapted from
https://github.com/ansible/ansible-examples/tree/master/jboss-standalone
which installs JBoss 7.1 and deploys the JBoss demo application "Ticket Monster".

- Creates a EC2 RHEL 7.2 instance
- Installs JBoss on that instance
- Deploys the Ticket Monster application

# Plays
 - Create EC2 Instances for JBoss Demo
 - Install JBoss and Deploy Apps

# Roles
- ec2_common
- jboss-standalone
- java-app

# Vars
- group_vars - EC2 specifics and JBoss ports

# Requirements
- AWS Account and parameters

# Tags
- provision
- install
- deploy

## Using this playbook
This playbook was created for Ansible Tower, uses Tower variables, and will require modifications to run
with Ansible Core.

- Modify group_vars/all with your own AWS Account parameters
- Create Tower configuration with specified parameters (below)
- Launch provisioning template
- Wait at least 1 minute for inventory to refresh
- Launch install/deploy template
- Navigate to http://<JBoss Server>:8080/ticket-monster

# Ansible Tower
- Add Project - https://github.com/bhirsch70/aws-jboss
- Configure AWS cloud credential
- Configure ec2-user machine credential
- Create EC2 dynamic inventory and 1 minute refresh schedule

- Create `ec2 provision` template:
  - `aws` credential
  - `ec2` inventory
  - `aws-jboss` project
  - `site.yml` playbook
  - `provision` tag
- Optional:  Add Survey to prompt for `ec2_instance_count`

- Create `Install JBoss / Deploy App` template
  - `ec2-user` credential
  - `ec2` inventory
  - `aws-jboss` project
  - `site.yml` playbook
  - `install,deploy` tags

-
