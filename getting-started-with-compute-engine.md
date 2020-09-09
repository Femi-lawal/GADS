# [LAB: Google Cloud Fundamentals: Getting Started with Compute Engine](https://googlepluralsight.qwiklabs.com/focuses/10168816?parent=lti_session)

## Objectives:
In this lab, you will learn how to perform the following tasks:
 - Create a Compute Engine virtual machine using the Google Cloud Platform (GCP) Console.
 - Create a Compute Engine virtual machine using the gcloud command-line interface.
 - Connect between the two instances.

## Steps: 

1. Create a Compute Engine Virtual Machiine using the GCP Console
      ```
      gcloud compute instances create "my-vm-1" \
      --machine-type "n1-standard-1" \
      --image-project "debian-cloud" \
      --image "debian-9-stretch-v20190213" \
      --subnet "default" --tags http
      ```
      ```
      gcloud compute firewall-rules create allow-http --action=ALLOW --destination=INGRESS --rules=http:80  --target-tags=http
      ```

2. Create a virtual machine using the gcloud command line
   - To display a list of all the zones in the region to which Qwiklabs assigned you, enter this partial command 
      ```
      gcloud compute zones list | grep us-central1
      ```
   - To set your default zone to the one you just chose, enter this partial command gcloud config set compute/zone followed by the zone you chose.
      Your completed command will look like this:
      ```
      gcloud config set compute/zone us-central1-b
      ```
   - To create a VM instance called my-vm-2 in that zone, execute this command:
      ```
      gcloud compute instances create "my-vm-2" \
      --machine-type "n1-standard-1" \
      --image-project "debian-cloud" \
      --image "debian-9-stretch-v20190213" \
      --subnet "default"
      ```

3. Connect between VM instances
   - Connect to my-vm-2:
      ```
      gcloud compute ssh my-vm-2
      ```
   - Use the ping command to confirm that my-vm-2 can reach my-vm-1 over the network:
      ```
      ping -c my-vm-1
      ```
   - Press Ctrl+C to abort the ping command. Use the ssh command to open a command prompt on my-vm-1:
      ```
      ssh my-vm-1
      ```
   - At the command prompt on my-vm-1, install the Nginx web server:
      ```
      sudo apt-get install nginx-light -y
      ```
   - Use the nano text editor to add a custom message to the home page of the web server:
      ```
      sudo nano /var/www/html/index.nginx-debian.html
      ```
   - Use the arrow keys to move the cursor to the line just below the h1 header. Add text like this, and replace YOUR_NAME with your name:
      ```
      Hi from YOUR_NAME
      ```
   - Press Ctrl+O and then press Enter to save your edited file, and then press Ctrl+X to exit the nano text editor.
      Confirm that the web server is serving your new page. At the command prompt on my-vm-1, execute this command:
      ```
      curl http://localhost/
      ```
   - To exit the command prompt on my-vm-1:
      ```
      exit
      ```
   - To confirm that my-vm-2 can reach the web server on my-vm-1, at the command prompt on my-vm-2, execute this command:
      ```
      curl http://my-vm-1/
      ```
4. Get the external IP of my-vm-1:
      ```
      gcloud compute instances list
      ```
5. Paste the copied IP address of my-vm-1 into a new browser tab and hit enter      
 