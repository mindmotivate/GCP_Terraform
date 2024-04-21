## GCP Terraform Authentication

**Step 1: Create a Service Account***

1. Log in to your Google Cloud Platform (GCP) account.
2. In the search bar, type "Service Accounts" and select it.
3. Click on "Create Service Account" and fill in the required details (name and description).
4. Click "Create" and continue. Grant the service account permissions by selecting a role (e.g., Owner or Editor).
5. Click "Done" to complete the process.
   
![Image20240421175752](https://github.com/mindmotivate/GCP_Terraform/assets/130941970/4094e37f-f1a5-4ca5-84b6-07e14fe4073e)

<img src="https://github.com/mindmotivate/GCP_Terraform/assets/130941970/4094e37f-f1a5-4ca5-84b6-07e14fe4073e" alt="Image20240421175752" width="50%">

<div style="text-align: left; margin-left: 2000px;"><img src="https://github.com/mindmotivate/GCP_Terraform/assets/130941970/4094e37f-f1a5-4ca5-84b6-07e14fe4073e" alt="Image20240421175752" width="50%"></div>


**Step 2: Create a Key**

> Navigate to the service account you just created.
> Under "Keys," click "Add Key" and select the JSON key type.
> GCP will generate and download the key in JSON format. Keep this file secure

**Step 3: Connect Terraform**

- Go to the Terraform Providers page on the Terraform website.
- Select Google Cloud Platform (GCP) and click "Use Provider" to copy the provider configuration code.

**Step 4: Set Up Terraform Project**

1. Open Visual Studio Code and create a new Terraform project.
2. Create a directory structure (e.g., `terraform/GCP/Humzamaroc`) and open it in Visual Studio Code.
3. Create a new file named `main.tf` and paste the copied provider configuration code into it.
4. Move the downloaded JSON key file to the workspace directory in Visual Studio Code.

**Step 5: Configure Terraform**

1. In the `main.tf` file, specify the following parameters:
   - `project`: The GCP project ID (found in the JSON key file).
   - `region`: The GCP region where resources will be deployed (e.g., `us-central1`).
   - `credentials`: The file name of the JSON key file.

**Step 6: Terraform Commands**

1. Use the terminal in Visual Studio Code to run Terraform commands:
   - `terraform validate`: Authenticate with GCP and validate the Terraform configuration.
   - `terraform plan`: Check the plan for deploying resources.
   - `terraform apply`: Apply the `main.tf` configuration to GCP and create a Terraform state file.

**Step 7: Create a GCS Bucket**

1. Go to the Terraform Registry documentation and search for "Cloud Storage."
2. Copy the code for creating a GCS bucket and paste it into the `main.tf` file below the credentials configuration.

**Step 8: Save and Apply Changes**

1. Save the `main.tf` file.
2. Run `terraform validate`, `terraform plan`, and `terraform apply` to authenticate with GCP, check the plan, and apply the configuration, respectively.

By following these steps, you can authenticate Terraform with GCP, configure a Terraform project, and deploy resources such as a Google Cloud Storage bucket using Terraform.



***This is how you show code:***


```hcl
resource "google_storage_bucket" "static-site" {
  name          = "image-store.com"
  location      = "EU"
  force_destroy = true

  uniform_bucket_level_access = true

  website {
    main_page_suffix = "index.html"
    not_found_page   = "404.html"
  }
  cors {
    origin          = ["http://image-store.com"]
    method          = ["GET", "HEAD", "PUT", "POST", "DELETE"]
    response_header = ["*"]
    max_age_seconds = 3600
  }
}
```



