

Official AWX git repo 
https://github.com/ansible/awx/

Create a 2 node (1 Master - 1 worker) Kubernetes cluster 
The size of node should be at least 4 GB RAM and 2 core CPU (t2.medium instance)
Untaint the master node so that it can create pods 

Follow the instructions in the link below  
https://github.com/ansible/awx/blob/devel/INSTALL.md

Some of the main things to be careful is - 

https://github.com/ansible/awx/blob/devel/installer/roles/kubernetes/defaults/main.yml
