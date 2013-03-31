Ansible EC2 Play Framework
=============

This is a set of Ansible scripts to deploy Play 2 projects in EC2 instances.

Steps to use:

* edit `hosts.ini` and set your ec2 instance(s) name
* edit `config/postfix_selections` to set domains for email 
* Add Amazon AWS keys to your ssh repository:

    ssh-agent
    
    ssh-add ~/path/to/foo.pem

* Run the ansible scripts:

    ansible-playbook -i hosts.ini <script>.yaml -u ubuntu (--sudo)


Scripts
=========
Scripts may contain variables that need to be customized for your specific deployments. The following scripts are available:

* bootstrap.yaml: secures an EC2 Ubuntu AMI using steps taken from. Requires sudo.
* playenv.yaml: sets play dependencies (pvm, java) and creates (via iptables) a mapping between port 80 and 9000 so Play doesn't require root privileges to run. Requires sudo.
* deploy.yaml: clones a Play project from a Git repository and deploys it on the machine. No sudo required.

WARNING: I'm no sysadmin, so the scripts may contain some big mistake (especially in the security part), so be careful when executing them and be sure you understand what you are doing.

Sources
=========

The original source which inspired most of these scripts: https://github.com/phred/5minbootstrap

A blog post that the author of 5minbootstrap wrote. Check it out! http://practicalops.com/my-first-5-minutes-on-a-server.html

This excellent post: http://plusbryan.com/my-first-5-minutes-on-a-server-or-essential-security-for-linux-servers




