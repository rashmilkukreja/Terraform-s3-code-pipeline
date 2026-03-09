# Terraform AWS S3 Static Website (CV Hosting)

This project uses **Terraform** to provision an **AWS S3 bucket configured as a static website** and deploy a CV / résumé website to it.
For more details refer [Medium]( https://medium.com/@lasisiabioduntowobola/deploying-a-static-website-to-aws-s3-using-terraform-and-github-actions-8bc932311d79)

The Terraform configuration automatically:

* Creates an **S3 bucket**
* Enables **public access for website hosting**
* Applies a **bucket policy for public read**
* Configures **S3 static website hosting**
* Uploads all website files from the `cv/` directory
* Outputs the **public website URL**

---

# Architecture

Terraform provisions the following resources:

* `aws_s3_bucket` – Creates the S3 bucket
* `aws_s3_bucket_acl` – Sets public read permissions
* `aws_s3_bucket_public_access_block` – Configures public access settings
* `aws_s3_bucket_policy` – Allows public read access to objects
* `aws_s3_bucket_website_configuration` – Enables static website hosting
* `aws_s3_object` – Uploads website files to the bucket
* `hashicorp/dir/template` module – Reads all files from the `cv` directory

---

# Project Structure

```
.
├── main.tf          # Core infrastructure resources
├── variables.tf     # Input variables
├── outputs.tf       # Terraform outputs
├── versions.tf      # Provider configuration
├── cv/              # Static website files
└── terraform.tfstate
```

### Terraform Files

**main.tf**

Defines:

* S3 bucket
* Access policies
* Static website configuration
* File uploads

**variables.tf**

Contains configurable parameters such as:

```
my_bucket_region
my_bucket_name
```

**outputs.tf**

Outputs the deployed website endpoint.

**versions.tf**

Defines the AWS provider configuration.

---

# Prerequisites

Before running this project, install:

* **Terraform**
* **AWS CLI**
* AWS account with permissions to create S3 resources

Authenticate AWS:

```
aws configure
```

---

# Usage

### 1. Initialize Terraform

```
terraform init
```

This downloads the required providers and modules.

---

### 2. Review the Plan

```
terraform plan
```

Shows the infrastructure Terraform will create.

---

### 3. Deploy Infrastructure

```
terraform apply
```

Type `yes` when prompted.

Terraform will:

* Create the S3 bucket
* Upload all files from the `cv` directory
* Enable static hosting

---

# Output

After deployment Terraform prints:

```
website_url = <your website URL>
```

Example:

```
http://your-bucket-name.s3-website.eu-north-1.amazonaws.com
```

Open this URL in your browser to view the deployed CV website.

---

# Customization

You can change values in `variables.tf`.

Example:

```
variable "my_bucket_region" {
  default = "eu-north-1"
}

variable "my_bucket_name" {
  default = "my-cv-website"
}
```

Or override them using a `.tfvars` file.

---

# Destroy Infrastructure

To remove all resources:

```
terraform destroy
```

---

# Notes

* The bucket is configured for **public read access** to allow website hosting.
* The `hashicorp/dir/template` module automatically uploads all files in the `cv` directory.
* Ensure the `index.html` file exists in the website directory.

---

# Author

Terraform project for hosting a **static CV website on AWS S3**.
