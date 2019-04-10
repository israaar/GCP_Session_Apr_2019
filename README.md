# GCP_Session_Apr_2019
A brief introduction to GCP.

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

ssh my-vm-1

ping my-vm-2
```
