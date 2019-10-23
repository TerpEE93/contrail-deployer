contrail-deployer
-----------------
This is an Ansible playbook that will speed deployment of a Contrail
Enterprise Multicloud cluster.  It assumes the following:

- One or more Command nodes
- One or more Controller nodes
- One or more Analytics (Appformix) nodes

The playbook will use the first (or only) Command node as the Command
deployer node as well.

The playbook assumes you have already imaged the hosts with a proper
release of CENTOS using the minimal ISO, enabled the root account on
each, and have IP addresses and routes associated with the correct
interfaces on each host.

The playbook will generate an SSH keypair and copy the files to the
/root/.ssh directory on each host.  It will scan each host for its
SSH fingerprint and add the results to a known_hosts file that will
be copied to /root/.ssh on each host.  It will also generate and copy
a proper /etc/hosts file to each node.

The playbook will 'yum install' the proper packages needed by
each host.  It will generate the command_servers.yml file needed
by the Deployer and copy it to /root on the Deployer node.  It will
also copy the files in the local ./files/appformix/ directory to
/opt/software/appformix on the Deployer node.  Then it will pull the
contrail_command_deployer container to the Deployer node and run it.

When complete, you will have a working instance of Contrail Command,
and you will be ready to deploy the rest of the environment from the
Command UI.