>⚠️ PLEASE SUBSCRIBE OUR CHANNEL [QwikCloud](https://www.youtube.com/@qwikcloud)
# GSP211
## Run in cloudshell (ZONE from Task 2, Step 3)
```cmd
#Exporting the Zone
export ZONE=
```
### Get REGION from task 1 point 3 (Create the privatenet network)
```cmd
# Exporting the region
export REGION2=
```
```cmd
#Exporting the Region
export REGION=${ZONE::-2}

#Creating privatenet
gcloud compute networks create managementnet --subnet-mode=custom

#Creating privatenet-region
gcloud compute networks subnets create managementsubnet-$REGION --network=managementnet --region=$REGION --range=10.130.0.0/20

#Creating a privatenet network
gcloud compute networks create privatenet --subnet-mode=custom

#Creating a privatenet-subnet
gcloud compute networks subnets create privatesubnet-$REGION --network=privatenet --region=$REGION --range=172.16.0.0/24
gcloud compute networks subnets create privatesubnet-$REGION2 --network=privatenet --region=$REGION2 --range=172.20.0.0/20

#Creating firewall rule
gcloud compute firewall-rules create managementnet-allow-icmp-ssh-rdp --direction=INGRESS --priority=1000 --network=managementnet --action=ALLOW --rules=icmp,tcp:22,tcp:3389 --source-ranges=0.0.0.0/0
gcloud compute firewall-rules create privatenet-allow-icmp-ssh-rdp --direction=INGRESS --priority=1000 --network=privatenet --action=ALLOW --rules=icmp,tcp:22,tcp:3389 --source-ranges=0.0.0.0/0

#Creating VM Instances
gcloud compute instances create	managementnet-${REGION}-vm --zone=$ZONE --machine-type=e2-micro --subnet=managementsubnet-$REGION
gcloud compute instances create privatenet-${REGION}-vm --zone=$ZONE --machine-type=e2-micro --subnet=privatesubnet-$REGION

#Creating vm-appliance
gcloud compute instances create vm-appliance \
--zone=$ZONE \
--machine-type=e2-standard-4 \
--network-interface=network-tier=PREMIUM,stack-type=IPV4_ONLY,subnet=privatesubnet-$REGION \
--network-interface=network-tier=PREMIUM,stack-type=IPV4_ONLY,subnet=managementsubnet-$REGION \
--network-interface=network-tier=PREMIUM,stack-type=IPV4_ONLY,subnet=mynetwork
```