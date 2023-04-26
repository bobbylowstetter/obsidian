Hosting a website on Google Cloud via Terraform and Docker.

# Prerequisites
- Github knowledge
- An active project in Google Cloud
- Terraform installed locally to your machine

# Finding what information we need in GCP
We need our project ID for use in our terraform code
- Go to [Google Cloud](https://console.cloud.google.com) 
	- Get to your home dashboard if you are not already there. To do so, just click on Google Cloud on the top left of your browser window.
- Take note of your project ID (not the project number)

# Create a service account
This account is what we will use to provide privileges to our terraform code
- Go to the Google Cloud Console ([https://console.cloud.google.com](https://console.cloud.google.com)).
- In the top navigation bar, select the project for which you want to create a service account.
- Click on the "IAM & admin" option from the left-hand menu.
- Click on the "Service accounts" option.
- Click on the "+ CREATE SERVICE ACCOUNT" button.
- Enter a name for your service account in the "Service account name" field.
- Optionally, enter a description for your service account in the "Service account description" field.
- Click on the "CREATE" button.
- On the "Add Key" screen, select "JSON" as the key type.
- Click on the "CREATE" button. This will download a JSON key file to your computer.
- Save the JSON key file in a secure location, as you will need it later to authenticate with Google Cloud using Terraform.
- After creating the service account, you will be redirected to the IAM & admin > Service accounts page. Click on the three dots to the right of the newly created service account and click on "Manage keys".
- Click on "Add Key" and select "JSON".
- Save the JSON key file to your computer.
- To assign the "Editor" role to the service account, click on the three dots next to the newly created service account and click on "Add Members".
- Enter the email address of the service account and select the "Editor" role from the "Select a role" dropdown.
- Click on the "SAVE" button.

# Putting our Terraform code together
Now for the meat! We have everything we need to get our Terraform code working. This section will depict creation of our terraform code split amongst multiple files.

## Authenticating with GCP
This code will link our terraform code to our Google Project
```
provider "google" {
  credentials = file("<path-to-json-key-file>")
  project     = "<google-cloud-project-id>"
  region      = "us-central1"
}
```
 - Put the above code in a blank directory. Call this file `main.tf`

## Firewall rules
This code will allow HTTP/HTTPS/ICMP traffic to talk to our GCP setup. A note for securing later, you would likely want to use a separate network instead of `default` in the future.
```
resource "google_compute_firewall" "default" {

name = "allow-http-https-traffic"

network = "default"

  

allow {

protocol = "tcp"

ports = ["80","443"]

}

  

# allow icmp so that we can ping and check the server is reachable or not

allow {

protocol = "icmp"

}

  

source_ranges = ["0.0.0.0/0"]

}
```
- Put the above code in the same directory as our `main.tf` file. Let's call this one `firewall.tf`

## Create the demo_server in GCE (Google Compute Engine)
Now we will create a demo to show that we can create a website with our current terraform code. 

```
resource "google_compute_instance" "devopsart" {

name = "devopsart-vm"

machine_type = "n1-standard-1"

zone = "us-central1-a"

  

#give image project and image family

  

boot_disk {

initialize_params {

image = "gce-uefi-images/centos-7"

}

}

  

#give the startup command which need to execute after created an instance

  

metadata_startup_script = "sudo yum -y update; sudo yum -y install epel-release; sudo yum -y install nginx; sudo service nginx start;"

  

#Choose the default network

  

network_interface {

network = "default"

access_config {

}

}

}
```
- Let's put this code in the same directory and call it `demo_server.tf`

# Running and Testing our Terraform code
Now let's run this and ensure it all works! 

## Running our Terraform
- Run `terraform init`. This will install any dependencies we may need for our terraform code.
- Run `terraform plan`. This will let us know what our terraform is going to do. This is also a good way to look for any bugs or typos.
- Run `terraform apply` when you are ready to deploy all this code to GCP!
	- SIDE NOTE: If you no longer want your code up on GCP, run `terraform destroy`. This will remove it all from GCP. 

## Testing our Terraform
- Go to the Google Cloud Console ([https://console.cloud.google.com](https://console.cloud.google.com)).
- Go to Compute Engine > VM Instances
- Copy the External IP of your VM and paste it to a browser.
- If you see your website, everything worked! 
	- A note that it takes about 10 minutes for your VM to fully boot up. Be patient. Until then you will get connection errors from the site. 
	- Also ensure you are using http:// and note https:// for the purposes of this lab.

# References
- [DevOpsArt](https://www.devopsart.com/2019/08/terraform-installation-and-create.html) 
- [ChatGPT](https://chat.openai.com)