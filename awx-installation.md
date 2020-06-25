

Official AWX git repo 
https://github.com/ansible/awx/

## Setup the kubernetes cluster 

- Create a 2 node (1 Master - 1 worker) Kubernetes cluster 
- The size of node should be at least 4 GB RAM and 2 core CPU (t2.medium instance)

https://github.com/ashishrpandey/kubernetes-training/blob/master/00installation.md

- Untaint the master node so that it can create pods 

        kubectl taint nodes --all node-role.kubernetes.io/master-


- Follow the instructions in the link below  
        https://github.com/ansible/awx/blob/devel/INSTALL.md

## Some of the main things to be careful during the installation - 

- Install Helm3 by following the link below 
https://github.com/ashishrpandey/kubernetes-training/blob/master/helm/helm3-installation.md

- No need to install Node, rest other packages needs to be installed as directed in https://github.com/ansible/awx/blob/devel/INSTALL.md#prerequisites

- Open the file
  https://github.com/ansible/awx/blob/devel/installer/inventory
  
  - Make the value of  kubernetes_context to the value of the current-context of your kubernetes cluster (use "kubectl config view")
  - Do not touch docker_registry_

- Open the file 
  https://github.com/ansible/awx/blob/devel/installer/roles/kubernetes/defaults/main.yml
  
- Change the values of the below parameters to these new values (Otherwise the pods would not be created) 

        web_cpu_request: 200
        task_mem_request: 1
        task_cpu_request: 200
        redis_mem_request: 1
        redis_cpu_request: 200

- Create a PV with 10 GB storage space. Modify the storage size to be 10 GB and use the file given below

    https://github.com/ashishrpandey/kubernetes-training/blob/master/06-storage/mongodb-pv-hostpath.yaml
    
 
- Execute the following to install AWX 
              
              $ ansible-playbook -i inventory install.yml
              $ kubectl get pods --namespace awx
              $ kubectl get svc --namespace awx

  
 
  ## Access the AWX web UI
    
-  As opposed to what is written in the README of AWX, there were 3 pods created in AWX namespace. 

- Use NodePort service named as awx-web-svc to access web UI
- Username is "admin" and the password is "password"
