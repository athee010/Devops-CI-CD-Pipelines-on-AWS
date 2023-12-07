# Setup Kubernetes on Amazon EKS

(https://docs.aws.amazon.com/eks/latest/userguide/getting-started-eksctl.html)   

####  
  - Inside EC2 Instance 
  
1. Setup kubectl   
   a. Download kubectl version 1.21  
   b. Grant execution permissions to kubectl executable   
   c. Move kubectl onto /usr/local/bin   
   d. Test that your kubectl installation was successful    


   curl -o kubectl https://amazon-eks.s3.us-west-2.amazonaws.com/1.21.2/2021-07-05/bin/linux/amd64/kubectl
   chmod +x ./kubectl
   mv ./kubectl /usr/local/bin 
   kubectl --version
   
2. Setup eksctl   
   a. Download and extract the latest release   
   b. Move the extracted binary to /usr/local/bin   
   c. Test that your eksclt installation was successful   

   
   curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp
   sudo mv /tmp/eksctl /usr/local/bin
   eksctl version
     
3. Create an IAM Role and attach it to EC2 instance    
   
   In the AWS console
   IAM – Create role- EC2- EC2Fullaccess- Cloudformation-IAMfullaccess- Adminstrative access- Name it
   To attach IAM to EC2 INSTANCE 
   Select instance- Actions- Security – Select IAM

   
4. Create your cluster and nodes 
   
  
   eksctl create cluster --name athee010-cluster \
   --region ap-south-1 \
   --node-type t2.small \
   

5. To delete the EKS clsuter 
   
   eksctl delete cluster athee010 --region ap-south-1
   
   
6. Validate your cluster using by creating by checking nodes and by creating a pod 
   
   kubectl get nodes
   kubectl run tomcat --image=tomcat 
   
   
   #### Deploying Nginx pods on Kubernetes
1. Deploying Nginx Container
    ```sh
    kubectl create deployment  demo-nginx --image=nginx --replicas=2 --port=80
    # kubectl deployment regapp --image=athee010/regapp --replicas=2 --port=8080
    kubectl get all
    kubectl get pod
   ```

1. Expose the deployment as service. This will create an ELB in front of those 2 containers and allow us to publicly access them.
   ```sh
   kubectl expose deployment demo-nginx --port=80 --type=LoadBalancer
   # kubectl expose deployment regapp --port=8080 --type=LoadBalancer
   kubectl get services -o wide
   ```

