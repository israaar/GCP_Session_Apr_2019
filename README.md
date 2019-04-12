# GCP_Session_Apr_2019
A brief introduction to GCP.

Refer on Coursera - GCP Fundamentals: Core Infrastructure

## Basics
### List Zones

``` 
gcloud compute zones list
gcloud compute zones list | grep us-central1
```
### Set Zone to us-central1-c

```
gcloud config set compute/zone us-central1-c
```

### Create instances ssh and ping

```
gcloud compute instances create "my-vm-1"

gcloud compute instances create "my-vm-2"

gcloud compute ssh my-vm-1

ping my-vm-2
```

### Install nginx and access home page from another server

```
sudo apt-get install nginx-light -y

sudo nano /var/www/html/index.nginx-debian.html

curl http://localhost

curl http://my-vm-1/
```

## Compute Engine
### Create instance 

```
gcloud compute instances create "my-vm-3" \
--machine-type "n1-standard-1" \
--image-project "debian-cloud" \
--image "debian-9-stretch-v20190213" \
--subnet "default"
```

## Cloud Storage

### Instance Setup for Demo 

Compute Engine -> VM instance -> Create -> Name it -> Region+Zone -> default Machine Type -> Boot Disk (Image) = Debian GNU/Linux 9(stretch) -> Identity and API access -> Firewall = Allow HTTP traffic-> Management, security, disks, networking, sole tenancy -> Startup script

```
apt-get update
apt-get install apache2 php php-mysql -y
service apache2 restart
```

### Cloud Storage bucket

```
#Cloud Shell
export LOCATION=US

#make a bucket after your projectID env var
gsutil mb -l $LOCATION gs://$DEVSHELL_PROJECT_ID

#retrieve a banner image from a publicly accessible Cloud Storage location
gsutil cp gs://cloud-training/gcpfci/my-excellent-blog.png my-excellent-blog.png

#copy banner to newly created CStore bucket
gsutil cp my-excellent-blog.png gs://$DEVSHELL_PROJECT_ID/my-excellent-blog.png

#publicy available to all
gsutil acl ch -u allUsers:R gs://$DEVSHELL_PROJECT_ID/my-excellent-blog.png

```

## Kubernetes Engine
### Start a cluster, Deploy a container, Run Services & Expose, Replicate.
```
export MY_ZONE=us-central1-a

#Start a cluster and configure it to run 2 nodes.
gcloud container clusters create webfrontend --zone $MY_ZONE --num-nodes 2

#Kubernetes container runs in pods
#Deploying a single pod containing nginx container. 
kubectl run nginx --image=nginx:1.10.0

kubectl get pods

#expose to internet
kubectl expose deployment nginx --port 80 --type LoadBalancer

kubectl get services

#scale to 3 pods
kubectl scale deployment nginx --replicas 3

kubectl get pods

kubectl get services
```

## App Engine
### Get an App Engine Application, launch, test and deploy to App Engine.

```
git clone https://github.com/GoogleCloudPlatform/appengine-guestbook-python

cd appengine-guestbook-python

ls -l

#template file
cat app.yaml

#Do web Preview in cloud shell after starting
dev_appserver.py ./app.yaml

#Deploy to App engine
gcloud app deploy ./index.yaml ./app.yaml

#View on internet
https://PROJECT_ID.appspot.com/
```
