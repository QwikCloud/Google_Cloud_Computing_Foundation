#Setup for second user
export USERNAME2=

#Create a file
touch sample.txt

#Create a bucket
gsutil mb gs://$DEVSHELL_PROJECT_ID

#Importing a file
gsutil cp sample.txt gs://$DEVSHELL_PROJECT_ID

#Revoking the viewr role for user2
gcloud projects remove-iam-policy-binding $DEVSHELL_PROJECT_ID --member="user:$USERNAME2" --role="roles/viewer"

#Granting the user2 permission for viewing object
gcloud projects add-iam-policy-binding $DEVSHELL_PROJECT_ID --member="user:$USERNAME2" --role="roles/storage.objectViewer"
