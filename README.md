# AnsibleMaaS

Ansible dynamic inventory script written in python to pull inventory from Canonical MaaS. <br>

Simple inventory that creates instance json records with MaaS attributes <br>


**Prerequisites:** <br>
1. A deployed instance of Cononical's MaaS v2.7 or better.<br>
2. Ansible v2.9 or newer installed and configured on a server/vm that has network access to the MaaS APIs.<br>
3. Python3 installed on the Ansible server(Control/Tower)/vm.<br>
4. Network access to the MaaS API URL and an API Key.<br>
<br>
<br>
**Dependencies**<br>
Python libs: <br>
- ansible<br>
- libmaas<br><br>
- json <br>
- packaging<br>
- os<br>
**To Install:** <br>
1. Clone this git repo.
>git clone https://git.halo.inc/halo-external/ansiblemaas.git <br>
2. Install the dependencies.<br>
> cd ansiblemaas <br>
> sudo pip install -r requirements.txt<br>
3. Copy the AnsibleMaaS.py file to the directory where you manage your ansible dynamic inventory.<br>
Normally: "/etc/ansible/inventory" <br>
4. **Set environment varibles!!** <br>
  **Change:** <br><br>
export MAAS_API_KEY=APIKEY-TO-ACCESS-MAAS-API #  <br>
export MAAS_URL=http://(IP or FQDN):5240/MAAS/api/2.0 # FQDN and URL of your MaaS Region API. <br>
<br>
Edit AnsiblMaaS.py to set options: <br>
sort_by_tags = "True"            # "True" will create a host group for each tag<br>
group_by_az = "True"             # "True" will create a host group for each availibility zone<br>
group_by_pool = "True"           # "True" will create a host group for each resource pool<br>
include_bare_metal = "True"      # "True" will include KVM hosts in the inventory<br>
include_host_details = "True".   # Will include all known facts from MaaS into the inventory<br>
<br>
# ansible_user to be used for differing OSs
ubuntu_user = "ubuntu"          # Default ansible user<br>
centos7_user = "centos"<br>
centos8_user = "cloud-user"<br>
windows_user = "cloud-admin"<br>


