# [LAB: Google Cloud Fundamentals: Getting Started with GKE](https://googlepluralsight.qwiklabs.com/focuses/10949195?parent=lti_session)

## Objectives:
In this lab, you will learn how to perform the following tasks:
 - Provision a Kubernetes cluster using Kubernetes Engine.
 - Deploy and manage Docker containers using kubectl.

## Steps: 

1. Confirm that needed APIs are enabled
   - Get a list of all enabled services
      ```
      gcloud services list --available
      ```
   - Scroll down in the list of enabled APIs, and confirm that both of these APIs are enabled:
      - Kubernetes Engine API
      - Container Registry API
   - If either API is missing, type the following command(replace SERVICE_NAME with the missing API name
      ```
      gcloud services enable SERVICE_NAME
      ```
2. Start a Kubernetes Engine cluster
   - To display a list of all the zones in the region to which Qwiklabs assigned you, enter this partial command 
      ```
      gcloud compute zones list | grep us-central1
      ```
   - Place your assigned zone in an environmental variable
      ```
      export MY_ZONE=us-central1-a
      ```
   - Start a Kubernetes cluster managed by Kubernetes Engine. Name the cluster webfrontend and configure it to run 2 nodes:
      ```
      gcloud container clusters create webfrontend --zone $MY_ZONE --num-nodes 2
      ```
   - After the cluster is created, check your installed version of Kubernetes using the kubectl version command:
      ```
      kubectl version
      ```

3. Run and deploy a container
   - From your Cloud Shell prompt, launch a single instance of the nginx container. (Nginx is a popular web server.)
      ```
      kubectl create deploy nginx --image=nginx:1.17.10
      ```
   - View the pod running the nginx container:
      ```
      kubectl get pods
      ```
   - Expose the nginx container to the Internet:
      ```
      kubectl expose deployment nginx --port 80 --type LoadBalancer
      ```
   - View the new service:
      ```
      kubectl get services
      ```
   - Scale up the number of pods running on your service:
      ```
      kubectl scale deployment nginx --replicas 3
      ```
   - Confirm that Kubernetes has updated the number of pods:
      ```
      kubectl get pods
      ```
   - Confirm that your external IP address has not changed:
      ```
      kubectl get services
      ```   
 