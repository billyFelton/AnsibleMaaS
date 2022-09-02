# AnsibleMaaS

Ansible dynamic inventory script written in python to pull inventory from Canonical MaaS. <br>
Originally part of a larger integration effort with MaaS the inventory component was spun off on its own. <br>

Existing integrations with MaaS only provided a list of hosts and required complicated playbooks to implement any
form of automation. The plugins were slow sometimes taking more than 5 minutes to pull a handfull of host instances. 

We needed to be able to sort invnetory based off MaaS specific attributes and associations. Resource pools, availibility zones and simple tagging 
being the most relevant. 

We also needed to be able to sever dependencies on ansible plugins / libraries.

Simple inventory that creates instance json records with MaaS attributes <br>

## Prerequisites: <br>
1. A deployed instance of Cononical's MaaS v2.7 or better.<br>
2. Ansible v2.9 or newer installed and configured on a server/vm that has network access to the MaaS APIs.<br>
3. Python3 installed on the Ansible server(Control/Tower)/vm.<br>
4. Network access to the MaaS API URL and an API Key.<br>

## Dependencies: <br>
Python libs: <br>
- ansible<br>
- libmaas<br>
- json <br>
- packaging<br>
- os<br>

## To Install: <br>
1. Clone this git repo.
2. Install the dependencies.<br>
   > cd ansiblemaas <br>
   > sudo pip install -r requirements.txt<br>
3. Copy the AnsibleMaaS.py file to the directory where you manage your ansible dynamic inventory.<br>
  Normally: "/etc/ansible/inventory" <br>
  Read this if you need help - https://docs.ansible.com/ansible/latest/user_guide/intro_dynamic_inventory.html
4. Set environment varibles!!
   > export MAAS_API_KEY=APIKEY-TO-ACCESS-MAAS-API #  <br>
   > export MAAS_URL=http://(IP or FQDN):5240/MAAS/api/2.0 # FQDN and URL of your MaaS Region API. <br>
  
<br>

## Edit AnsiblMaaS.py to set options: <br>
sort_by_tags = "True"            # "True" will create a host group for each tag<br>
group_by_az = "True"             # "True" will create a host group for each availibility zone<br>
group_by_pool = "True"           # "True" will create a host group for each resource pool<br>
include_bare_metal = "True"      # "True" will include KVM hosts in the inventory<br>
include_host_details = "True".   # Will include all known facts from MaaS into the inventory<br>
<br>

### ansible_user to be used for differing OSs:
ubuntu_user = "ubuntu"        
centos7_user = "centos"<br>
centos8_user = "cloud-user"<br>
windows_user = "cloud-admin"<br>

Once everything is setup simply execute an ansible module against the inventory.
> ansible -m ping all

## Instance access issues.
MaaS deploys private keys on bare metal and vm instances. Whichever user is is running ansible must have public keys associated with ssh on
each instaance ansible will need to access. If you are unfamiliar with ansible, ansible-inventory or ssh, take the time to read the docs.<br>
Having a strategy on inventory and ssh is a good idea. Rotating keys, using secrets managment are generally a good idea. <br>
- Getting started with Ansible - https://docs.ansible.com/ansible/latest/getting_started/index.html <br>
- Ansible Connection Methods. - https://docs.ansible.com/ansible/latest/user_guide/connection_details.html <br>
