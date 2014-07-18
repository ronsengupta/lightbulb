# cloud

vagrant up node-1 node-2 node-3

This is our foray into dynamic inventories and provisioning cloud instances.  This example shows the following concepts:

* using mixed static/dynamic inventories
* using group_vars to set the remote user
* provisioning instances and using wait_for
* including playbooks within playbooks
* using extra vars


You'll need your AWS credentials configured either in ```$HOME/.boto``` or set in environment variables.  You'll also need your AWS ssh-key in your keychain (using ssh-add).  

We also wanto to show how to use extra vars, so there is a ansible-vaulted file named secrets.yml, with the password of: ```password```.  Changing this will override the test message on the web pages.

Will also have to discuss why this provisioning is a two step procedure and how ec2_groups are named

You'll also have to override my key_name parameter for the infra role to something that you actually have -- you could that with extra vars or by sending the parameter to the role.


Once that is setup, just run:

    #ensure that ec2 cache is purged
    rm -rf ~/.ansible/tmp/ansible-ec2.*
    
	# provision the infrastructure
	ansible-playbook infra.yml -e "key_name=my_ec2_key"
	
	# provision the apps
	ansible-playbook site.yml -e @secrets.yml --ask-vault-pass