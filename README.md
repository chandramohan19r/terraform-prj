# terraform-prj
terraform based resources creation 

# 📦 Terraform Module: AWS S3 Bucket with Versioning

This Terraform module provisions an AWS S3 bucket with versioning enabled and customizable tags.

## 🚀 Features

- Creates a private S3 bucket
- Enables versioning for object recovery
- Supports environment-based tagging

## 📥 Inputs

| Name         | Description                  | Type   | Required |
|--------------|------------------------------|--------|----------|
| bucket_name  | Name of the S3 bucket         | string | ✅ Yes   |
| environment  | Environment tag (e.g., dev)   | string | ✅ Yes   |

## 📤 Outputs

| Name       | Description             |
|------------|-------------------------|
| bucket_id  | ID of the created bucket |

## 🛠️ Usage

module "my_bucket" {
  source      = "./modules/s3_bucket"
  bucket_name = "chandramohan-devops-logs"
  environment = "dev"
}
