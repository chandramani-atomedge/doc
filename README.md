# RunBook documentation for running the Infra structure using terraform 

## Install Terraform on your local machine 
https://developer.hashicorp.com/terraform/install?product_intent=terraform

Select the OS we want to download and install the terraform

## Install AWS cli on our local machine 
https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html

Specify the OS which we want to download and install the aws cli

## Create a Access key and secret key in aws console

Login in to the aws console and create a access key for the specific user in the IAM 

## Configure AWS ClI on your machine
```
aws configure 
```

copy paste your access key and scret key which you have downloaded 


## Guided steps to run the terraform code 
### we need to run the terraform code in an order
At first we need to run the pipelines, then the monitoring server and finally the infrastructure 

## Pipeline Configuration
#### clone the git repo of our pipeline - https://github.com/atomedgesoft/Aura-Project-Deploy-Pipelines-Terraform.git

```
https://github.com/atomedgesoft/Aura-Project-Deploy-Pipelines-Terraform.git
```
Go to every folder and initialize the terrraform command, for exapmle
```
cd Backend-Deploy-Pipeline-Terraform/
```
Steps:
```
terraform init
```
```
terraform plan 
```
```
terraform apply -var="region=ap-south-1" --auto-approve
```

And change to another folder and then follow the above Steps to run the all four pipelines 

## Initaitate the Monitoring server
#### clone the git repo of the monitoring server - https://github.com/atomedgesoft/Aura-cloud-Monitoring.git 
```
git clone https://github.com/atomedgesoft/Aura-cloud-Monitoring.git
```
Go to the directory and run the terraform commands to initate our monitoring server
```
terraform init
```
```
terraform plan
```
```
terraform apply -var="region=ap-south-1" --auto-approve
```

## Guide to run the Infra 
#### clone the git repo of our infra - https://github.com/atomedgesoft/aura-cloud.git

```
git clone https://github.com/atomedgesoft/aura-cloud.git
```
##### Go to the Cloned directory and edit the terraform.tfvars file for our need 
Add the monitoring server ip in the terraform.tfvars file 

### Give the following command to run the infra in the selected account 
#### For Running the infra in the dev-account initialize the terraform code by using this command 
```
terraform init -backend-config="bucket=aura-backup-bucket" -backend-config="key=dev-account/terraform.tfstate" -backend-config="region=ap-south-1"
```
#### For Running the infra in the stage-account initialize the terraform code by using this command 

```
terraform init -backend-config="bucket=aura-backup-bucket" -backend-config="key=stage-account/terraform.tfstate" -backend-config="region=ap-south-1"
```
#### For Running the infra in the prod-account initialize the terraform code by using this command 

```
terraform init -backend-config="bucket=aura-backup-bucket" -backend-config="key=prod-account/terraform.tfstate" -backend-config="region=ap-south-1"
```

### Once Initialized create and select the workspace in which enviroment our infra need to run 
#### Create a new terraform workspace in the terminal by using this command 
```
terraform workspace new dev
```

```
terraform workspace new stage
```

```
terraform workspace new prod
```

#### We can list all the workspace by using this command 
```
terraform workspace list
```

#### Select the workspace once created
```
terraform workspace select <>
```
Eg:dev, stage, prod

#### After selecting the workspace validate our infra
```
terraform plan
```

#### Run the infra by using this command 
```
terraform apply -var="region=ap-south-1" --auto-approve
```
