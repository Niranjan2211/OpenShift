OpenShift
How to Install Openshift 3.11.

```
make sure you have 2 cpu and 8gb machine
vagrant init
vagrant up
make sure you have 2 cpu and 8gb machine
vagrant init
vagrant up

yum update -y
yum -y install git docker epel-release wget NetworkManager 
wget https://releases.ansible.com/ansible/rpm/release/epel-7-x86_64/ansible-2.6.5-1.el7.ans.noarch.rpm
yum localinstall ansible-2.6.5-1.el7.ans.noarch.rpm -y
systemctl start docker
systemctl enable docker
systemctl show NetworkManager | grep ActiveState
systemctl enable NetworkManager
systemctl start NetworkManager
systemctl status NetworkManager
systemctl show NetworkManager | grep ActiveState
systemctl stop firewalld
systemctl disable firewalld
cat /etc/selinux/config
getenforce
git clone https://github.com/openshift/openshift-ansible
cd openshift-ansible
git branch -r
git checkout release-3.9
# ssh-keygen 





# cat ~/.ssh/id_rsa.pub > ~/.ssh/authorized_keys
#cat /etc/ansible/hosts

[OSEv3:children]
masters
nodes
etcd

# Set variables common for all OSEv3 hosts
[OSEv3:vars]
# SSH user, this user should allow ssh based auth without requiring a password
ansible_ssh_user=root

# If ansible_ssh_user is not root, ansible_become must be set to true
#ansible_become=true

openshift_deployment_type=origin

# uncomment the following to enable htpasswd authentication; defaults to DenyAllPasswordIdentityProvider
openshift_master_identity_providers=[{'name': 'htpasswd_auth', 'login': 'true', 'challenge': 'true', 'kind': 'HTPasswdPasswordIdentityProvider'}]
openshift_master_htpasswd_users={'ocpadmin': '$apr1$6V7cwQUj$keza/4SteHQgKYT0HqL500'}
openshift_master_htpasswd_file='/etc/origin/master/htpasswd'

openshift_disable_check=disk_availability,package_availability,package_version,memory_availability,docker_image_availability
#openshift_disable_check=memory_availability,docker_image_availability

openshift_master_default_subdomain=openshift01.xyz.com
#openshift_install_examples=true
openshift_master_cluster_method=native
openshift_console_install=true
openshift_console_hostname=openshift01.xyz.com
openshift_master_cluster_public_hostname=openshift01.xyz.com
openshift_master_cluster_hostname=openshift01.xyz.com
openshift_master_console_port=443
openshift_master_api_port=443


# host group for masters
[masters]
openshift01.xyz.com

# host group for etcd
[etcd]
openshift01.xyz.com

# host group for nodes, includes region info
[nodes]
openshift01.xyz.com openshift_public_hostname=openshift01.xyz.com openshift_node_group_name='node-config-all-in-one'
[root@openshift01 ~]#



ansible-playbook playbooks/prerequisites.yml
ansible-playbook playbooks/deploy_cluster.yml
 this process will take 15 to 20 mins
 goto browser https://172.24.0.11:8443

# oc login -u system:admin
# oc get node
# oc get po -n default
oc get projects
oc get namespaces
oc projects
oc new-project new-project1
oc project default
oc delete project new-project1
oc new-app centos/ruby-22-centos7~https://github.com/openshift/ruby-ex.git
oc whoami
oc create user user1
oc get users
oc login -u developer
 oc new-project project1
oc new-app centos/ruby-22-centos7~https://github.com/openshift/ruby-ex.git
oc get pods
docker ps
oc get services
curl -I -m3 172.30.173.195:8080
oc delete svc/ruby-ex
oc get svc
oc expose pods/ruby-ex-1-zzhrc
oc get svc
curl -I -m3 172.30.111.104:8080
oc expose service/ruby-ex-1-zzhrc --hostname="openshiftdemo.local"
oc get routes
oc status

```
