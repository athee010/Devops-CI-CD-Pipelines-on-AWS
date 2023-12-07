# Integrating Kubernetes cluster with Ansible

### In the bootstrap image server

Add user ansadmin
useradd ansadmin
passwd ansadmin

add it in visudo

### Enable password based authentication

    vi /etc/ssh/sshd_config
    Password Authentication yes

  service sshd reload


### In the ansible server
Create images with the exisitng file and push it into the docjer 

sudo su -
cd /opt/docker 
ll
mv regapp.yml create_regapp.yml


### Update hosts file with new group called kubernetes and ansible 
    vi hosts

    kubernetes
    [  ip   ]
    
    ansible 
    [  ip  ]

1. Login to ansible server and copy public key onto kubernetes cluseter master account 
    
    ssh-copy-id <ip of kubernetes>


    ssh-copy-id root@<ansible server ip>


vi kubedeploy.yml

---
- hosts: kubernetes
#  become: ture
  user: root

  tasks:
    - name: deploy regapp on kubernetes
      command: kubectl apply -f regapp-deployment.yml

    - name: create service for regapp
      command: kubectl apply -f regapp-service.yml

    - name: update deployment with new pods if image updated in docker hub
      command: kubectl rollout restart deployment.apps/athee010-regapp


ansible-playbook -i /opt/docker/hosts kubedeploy.yml

### In the bootstrap server
    kubectl get all
