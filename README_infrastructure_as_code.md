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





