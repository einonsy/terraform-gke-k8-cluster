If running for the first time: 
brew cask install google-cloud-sdk    

To authenticate with GCP
gcloud init

To allow terraform access to the credentials: 
gcloud auth application-default login

To find the cloud project run
gcloud config get-value project

If no project is set run 
gcloud config set project {project name}

Once you are happy with the config run 
Terraform plan
Terraform apply    

If this is a first run in an account there is likely to be various api failures as all the required google api’s will not be enabled. 

Once terraform has run to get the details of the cluster run: 
gcloud container clusters get-credentials proj-einonsy01-gke --region Europe-west2


Deploying the kubernetes dashboard to check health of cluster (this uses kubectl)

kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.0.0-beta8/aio/deploy/recommended.yaml

Run a local cube proxy
Kubectl proxy

Create a user to access the proxy
kubectl apply -f https://raw.githubusercontent.com/hashicorp/learn-terraform-provision-eks-cluster/master/kubernetes-dashboard-admin.rbac.yaml

Generate auth token
kubectl -n kube-system describe secret $(kubectl -n kube-system get secret | grep service-controller-token | awk '{print $1}')
