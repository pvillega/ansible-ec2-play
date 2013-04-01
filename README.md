# Ansible EC2 Play Framework

This is a set of Ansible scripts to deploy Play 2 projects in EC2 instances.

Steps to use:

* edit `hosts.ini` and set your ec2 instance(s) name
* edit `config/postfix_selections` to set domains for email 
* Add Amazon AWS keys to your ssh repository:
 
    ssh-agent    
    ssh-add ~/path/to/foo.pem

* Run the ansible scripts:

    ansible-playbook -i hosts.ini script_name.yaml -u ubuntu (--sudo)

And done. Your EC2 isntance should be ready to go.

## Scripts

Scripts may contain variables that need to be customized for your specific deployments. The following scripts are available:

* bootstrap.yaml: secures an EC2 Ubuntu AMI. Requires sudo.
* playenv.yaml: sets play dependencies (pvm, java) including Authbind so Play can use port 80 without root privileges. Requires sudo.
* deploy.yaml: clones a Play project from a Git repository and deploys it on the machine. No sudo required.


WARNING: I'm no sysadmin, so the scripts may contain some big mistake (especially in the security part), so be careful when executing them and be sure you understand what you are doing.
WARNING: if you use a Micro EC2 instance the deployment script will fail (ubuntu will kill the build due to lack of memory), you will need to do that part manually



## Start file

The settings assume the use of [Authbind](http://en.wikipedia.org/wiki/Authbind) so Play can run on port 80 without root privileges. A `start` file is provided under folder `exec` that can be used as a template for your own `start` file.

Deployment scripts assume you place your customized `start` file at the root of the project cloned via git. Modify the script accordingly if that's not the case.

## Sources


The original source which inspired most of these scripts: https://github.com/phred/5minbootstrap

A blog post that the author of 5minbootstrap wrote. Check it out! http://practicalops.com/my-first-5-minutes-on-a-server.html

This excellent post: http://plusbryan.com/my-first-5-minutes-on-a-server-or-essential-security-for-linux-servers
