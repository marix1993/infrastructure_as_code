Infrastructure as code ( it's a way of codifying everything and every step).
-

###  What is IaC?

![iac_diagram.png](files%2Fiac_diagram.png)

- IaC stands for Infrastructure as Code. It means writing code to manage and provision infrastructure resources like servers, networks, and storage. This approach automates the deployment and configuration of infrastructure, making it easier to manage, scale, and replicate environments.

## Benefits of IaC:

- Consistency and repeatability: IaC allows for the automated provisioning and configuration of infrastructure resources in a consistent and repeatable way. This can reduce the likelihood of errors and ensure that infrastructure is set up correctly every time.

- Scalability: IaC can easily scale up or down depending on the demand. With IaC, infrastructure resources can be quickly created, modified, and deleted to meet the changing needs of an application or business.

- Speed and agility: IaC can significantly reduce the time required to provision and configure infrastructure. With IaC, teams can quickly and easily create new infrastructure environments or make changes to existing ones.

- Cost savings: IaC can help organizations save money by reducing the amount of time and effort required to manage infrastructure manually. This can free up resources for other important tasks.

- Collaboration and version control: IaC allows for infrastructure definitions to be version-controlled and stored in a source code repository, enabling teams to collaborate, review, and manage changes to infrastructure in the same way they do with application code.

- Compliance and security: IaC can help ensure that infrastructure resources are provisioned and configured in a compliant and secure manner. IaC can also help ensure that infrastructure resources are consistent with security policies and standards.

### Use cases:

- Provisioning and configuration of infrastructure: IaC is used to automate the creation and configuration of servers, networks, and other infrastructure components. This can include configuring operating systems, installing software, setting up firewalls, and creating user accounts. Cloud providers like AWS, Azure, and GCP offer IaC tools like CloudFormation, Azure Resource Manager, and Google Cloud Deployment Manager to help automate these tasks.

- Application deployment: IaC can be used to automate the deployment of applications to infrastructure resources. This can include installing software, configuring settings, and deploying code. Tools like Ansible, Chef, and Puppet can be used to manage application deployment across different environments.

- Testing and validation: IaC can be used to create and manage test environments, including infrastructure and applications. This can help automate testing and validation tasks, ensuring that changes are thoroughly tested before being deployed to production.

- Compliance and security: IaC can help ensure that infrastructure and applications meet security and compliance requirements. By automating the configuration of security settings and policies, IaC can help reduce the risk of security breaches and ensure that infrastructure is compliant with regulations like HIPAA or PCI DSS.

### How is it used in the industry?

- Some companies that use IaC include Netflix, Airbnb, and Google. These companies use IaC to manage large, complex environments and to scale their infrastructure efficiently. In addition, many startups and small businesses are adopting IaC to improve their infrastructure management and to reduce the time and effort required for infrastructure management tasks.

### Configuration management.

![conf_management.png](files%2Fconf_management.png)

- Configuration management is the process of managing and automating changes to infrastructure configurations, such as servers, applications, and network devices. Configuration management tools help track and manage changes, enforce consistency, and maintain desired configurations over time.

### What is Ansible?

![ansible.png](files%2Fansible.png)

- Ansible is a popular open-source configuration management and automation tool. It uses a simple syntax called YAML to define infrastructure resources and configurations in playbooks. Ansible can manage a wide range of devices and platforms, from servers to cloud resources, and has a large user community and ecosystem of modules and plugins. Some use cases for Ansible include configuration management, application deployment, and continuous delivery.

### What is YAML and playbooks?

- YAML (short for "YAML Ain't Markup Language") is a human-readable data serialization format. It's used in Ansible playbooks to define infrastructure resources and configurations in a structured way. 
- Playbooks are sets of instructions that define a series of tasks to be executed on remote hosts using Ansible. Playbooks can include conditionals, loops, and variables, making them a powerful way to automate complex workflows.

# IaC

## What is Iac?

- Infastructure As Code (IaC) is the managing and provisioning of your infrastructure through code instead of through manual processes.

## Benefits of IaC?

- Stable and scalable test environments.

- Low risk of human errors.
- Improved consistency.
- Improved security.
- Speed due to automation.

## Configuration management.
Configuration management is the process of managing and automating changes to infrastructure configurations. Configuration management tools help track and manage changes, enforce consistency, and maintain desired configurations over time.

## What is Ansible?
Ansible is a popular open-source configuration management and automation tool. It uses a simple syntax called YAML to define infrastructure resources and configurations in playbooks.

## What is YAML and Playbooks?
YAML (short for "YAML Ain't Markup Language") is a human-readable data serialization format. It's used in Ansible playbooks to define infrastructure resources and configurations in a structured way.

Playbooks are sets of instructions that define a series of tasks to be executed on remote hosts using Ansible. Playbooks can include conditionals, loops, and variables, making them a powerful way to automate complex workflows.

# Set Up Ansible Controller with Node/s

![ansible_controller_setup.png](files%2Fansible_controller_setup.png)

1. Firstly, download Vagrant on your local machine

2. Next, download Ruby on your local machine.
- For Windows:
    ```
    https://github.com/oneclick/rubyinstaller2/releases/download/RubyInstaller-2.6.6-1/rubyinstaller-devkit-2.6.6-1-x64.exe
    ```

- For Mac:
    ```
    https://www.ruby-lang.org/en/downloads/
    ```

3. Download Virtual Box on your local machine. Check what version you need first.
4. Download VS Code on your local machine.
5. Open VS Code and change directory to your folder. Run the command `vagrant init` to initialise a Vagrant file.
6. In your Vagrant file, delete what is in there and enter the following:
    ```
    Vagrant.configure("2") do |config|
    # creating are Ansible controller
    config.vm.define "controller" do |controller|
        
        controller.vm.box = "bento/ubuntu-18.04"
        
        controller.vm.hostname = 'controller'
        
        controller.vm.network :private_network, ip: "192.168.33.12"
        
        # config.hostsupdater.aliases = ["development.controller"] 
        
    end 
    # creating first VM called web  
    config.vm.define "web" do |web|
        
        web.vm.box = "bento/ubuntu-18.04"
        # downloading ubuntu 18.04 image
    
        web.vm.hostname = 'web'
        # assigning host name to the VM
        
        web.vm.network :private_network, ip: "192.168.33.10"
        #   assigning private IP
        
        #config.hostsupdater.aliases = ["development.web"]
        # creating a link called development.web so we can access web page with this link instread of an IP   
            
    end
    
    # creating second VM called db
    config.vm.define "db" do |db|
        
        db.vm.box = "bento/ubuntu-18.04"
        
        db.vm.hostname = 'db'
        
        db.vm.network :private_network, ip: "192.168.33.11"
        
        #config.hostsupdater.aliases = ["development.db"]     
    end
    
    
    end
    ```
7. Run the command `vagrant up` the launch your Virtual Box/Boxes.
8. SSH into your first virtual box with `vagrant ssh <box-name>`
9. Run `sudo apt update -y` to update your Virtual Box.
10. Run `sudo apt upgrade -y` to upgrade your Virtual Box.
11. Open 2 more terminal windows and follow from `step 8` to update and upgrade both Virtual Boxes.
12. In your controller box, check your python version and make sure it is 2.7 or higher. `python --version`
13. Run the following command to install software properties. `sudo apt install software-properties-common`
14. Now we need to add Ansible to our virtual box. `sudo apt add-repository ppa:ansible/ansible`. Press enter to confirm.
15. Update your Virtual Box again. `sudo apt update -y`
16. Now install Ansible onto your Virtual Box. `sudo apt install ansible -y`
17. Check your Ansible version. `sudo ansible --version`
18. To change directory between two Virtual Boxes. The password to enter is `vagrant` (The ip address for the Virtual Box can be found in your Vagrant file)
    ```
    ssh vagrant@<ip-address>
    ```

# Set Up Controller

## Launch Virtual Machines

1. Open terminal/bash window.

2. Change directory into where your vagrant file is.
3. Launch your Virtual Machines with the command `vagrant up`.
4. SSh into your controller VM `vagrant ssh controller`.
5. Now update and upgrade your machine. `sudo apt update -y && sudo apt upgrade -y`

## Test SSH Connection

1. Use the following command to ssh into your web machine from your controller machine. `ssh vagrant@<vm-ip-address>`

2. Run the following command to update and upgrade your machine. `sudo apt update -y && sudo apt upgrade -y`
3. Use the command `exit` to exit out your web machine back into your controller machine.
4. Use the following command to ssh into your db machine from your controller machine. `ssh vagrant@<vm-ip-address>`
5. Run the following command to update and upgrade your machine. `sudo apt update -y && sudo apt upgrade -y`
6. Use the command `exit` to exit out your web machine back into your controller machine.

## Set Up Controller Connection

1. Change directory into your ansible default directory. `cd /etc/ansible/`
2. Check what files/folder are in your current directory. `ls`
3. Using the following command we can see the layout of our directory more clearly. `sudo apt install tree` , `tree`
4. Open the hosts file with the following command. `sudo nano hosts`
5. In the file create two separate groups. One for your web machine and one for your db machine. The syntax is below.

    - ansible_connection=ssh is used to show how we want to connect.
    - ansible_ssh_user=vagrant is to show who the user is.
    - ansible_ssh_pass=vagrant is to tell what the password is.

    ```
    [web]
    192.168.33.10 ansible_connection=ssh ansible_ssh_user=vagrant ansible_ssh_pass=vagrant

    [db]
    192.168.33.11 ansible_connection=ssh ansible_ssh_user=vagrant ansible_ssh_pass=vagrant

    ```

- If we receive any error while adding DB connection we should use command `sudo nano
ansible.cfg` then add (NEVER DO THIS IN LIVE ENVIRONMENT) `host_key_checking = false`.

6. To check the connection is working between the controller machine and the web & db machine use the following command. `sudo ansible all -m ping`

![ansible_1.png](files%2Fansible_1.png)

- If you want to check the connection between one machine use the command `sudo ansible <box-name> -m ping`.

7. Ansible is powerful and to check information about machine use the following command. `sudo ansible all -a "<command>"`

- If you want to check information for one machine use the following command. `sudo ansible <box-name> -a "<command>"`

## Communicating with different nodes.

1. To check the date within the nodes. `sudo ansible all -a "date"`
2. To send created file from controller to a specific node we can use this command: 
`sudo ansible web -m copy -a "src=/etc/ansible/testing.txt dest=/home/vagrant"`

## Creating PlayBook 
(file containing a set of tasks and plays that define the automation that needs to be performed on a set of hosts)

1. We should start with creating a YAML file. `sudo nano install-nginx-playbook.yml`
2. Within this file we should add this code:

```commandline
# Creating a playbook to install nginx in web server 

# YAML file starts ---
---

# where would you like to install nginx
- hosts: web

# would you like to see logs
  gather_facts: yes

# do we need admin access - sudo
  become: true

# add the instructions - commands
  tasks:
  - name: Install nginx in web-server


    apt: pkg=nginx state=present
# ensure status is running/active
```
3. To run the PlayBook we can use this command. `sudo ansible-playbook install-nginx-playbook.yml `
4. To check if nginx is active. `sudo ansible web -a "systemctl status nginx"`

## Creating a PlayBook to run our Sparta Global App.

1. First step is to create YAML file to install all the dependencies to launch the app.`sudo nano install-nodejs-playbook.yml`
2. Now we should add slightly changed code:
```commandline
# YAML file starts ---
---

# where would you like to install nodejs
- hosts: web

# would you like to see logs
  gather_facts: yes

# do we need admin access - sudo
  become: true

# add the instructions - commands
  tasks:
  - name: Install Python in web-server
    apt: pkg=python state=present

  - name: Install node in web-server
    apt: pkg=nodejs state=present

  - name: Install npm in web-server
    apt: pkg=npm state=present
```
3. Now in second GitBash terminal navigate to folder where we have a `Vagrant file` and use command to secure copy `app` folder. `scp -r /c/Users/Mateusz/Documents/tech221/virtualisation/app vagrant@192.168.33.10:/home/vagrant`
4. Now slightly change the already created `install-nodejs-playbook.yml` by adding the following commands:

```commandline
# start the app
  - name: Start the application
    command:
      chdir: /home/vagrant/app
      cmd: npm start &
```
or you can do it manually by:
- ssh into web `ssh vagrant@192.168.33.10`
- navigating to app `cd app`
- starting the app `node app.js`

![works.png](files%2Fworks.png)
















































