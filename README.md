# 🏗️ Terraform-google-vm
# Google Cloud Infrastructure Provisioning with Terraform

[![Vikas](https://img.shields.io/badge/Made%20by-Vikas-blue?style=flat-square&logo=terraform)]
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Terraform](https://img.shields.io/badge/Terraform-1.13%2B-purple.svg?logo=terraform)](#)
[![CI](https://github.com/chahalvikas2022/terraform-gcp-vm/actions/workflows/ci.yml/badge.svg)](https://github.com/chahalvikas2022/terraform-gcp-vm/actions/workflows/ci.yml)
[![Latest Release](https://img.shields.io/github/release/chahalvikas2022/terraform-gcp-vm.svg)](https://github.com/chahalvikas2022/terraform-gcp-vm/releases/latest)

> 🌩️ **A production-grade, reusable GCP vm module by [Vikas]**
> Designed for reliability, performance, and security — following GCP networking best practices.
---

## 🏢 About Vikas

**Vikas** delivers **Cloud & DevOps excellence** for modern teams:
- 🚀 **Infrastructure Automation** with Terraform, Ansible & Kubernetes
- 💰 **Cost Optimization** via scaling & right-sizing
- 🛡️ **Security & Compliance** baked into CI/CD pipelines
- ⚙️ **Fully Managed Operations** across GCP, Azure, and AWS


---
## 🌟 Features

🔥 Terraform GCP VM Instance Module – Key Features

- ✅ Create highly configurable GCP VM instances with full support for machine type, zone, custom hostname, and metadata

- ✅ Seamless label management using the Vikas Multicloud Labels Module
     for consistent naming across environments

- ✅ Supports multiple VMs using instance_count with dynamic naming (name-1, name-2, …)

- ✅ Automatic boot disk configuration with customizable size, type, image, and labels

- ✅ Optional local SSD / scratch disks via dynamic blocks for high-performance workloads

- ✅ Enable Shielded VM configuration (secure boot, vTPM, integrity monitoring)

- ✅ Supports Network Performance Tier configuration for high-bandwidth workloads

- ✅ Full network flexibility:

  * Public IP (optional)
  
  * IPv6 support
  
  * Alias IP ranges
  
  * Custom NIC type, queue count, stack type

- ✅ Service Account support — attach service accounts + custom scopes as needed

- ✅ GPU / Accelerator support using dynamic guest_accelerator block

- ✅ Supports startup scripts with automatic logging at /var/log/startup-script.log

- ✅ VM naming, labeling, and metadata fully dynamic, driven by variables

- ✅ Built with best Terraform practices:

  * Idempotent design
  * Dynamic blocks for optional features
  * Clean variable-driven architecture

- ⚙️ Perfect for dev, stage, prod multi-environment deployments

---


## ⚙️ Usage Example
### 🧱  compute_instance Example
  ```hcl
      module "compute_instance" {
      source                 = "https://github.com/chahalvikas2022/terraform-gcp-vm.git"
      name                   = "dev"
      environment            = "test"
      instance_count         = 1
      zone                   = "asia-northeast1-a"
      instance_tags          = ["foo", "bar"]
      machine_type           = "e2-small"
      image                  = "ubuntu-2204-jammy-v20230908"
      service_account_scopes = ["cloud-platform"]
      subnetwork             = module.subnet.subnet_id
      network                = module.vpc.vpc_id
    
      enable_public_ip = true # Enable public IP only if enable_public_ip is true
      metadata = {
        ssh-keys = <<EOF
          ubuntu:ssh-rsa AAAAB3NzaCph/FXUAHBaekf+hzL58= suresh@suresh
        EOF
      }
    }
  
  ```
### ☁️ Outputs (GCP Compute Instances Module)

| **Name**              | **Description**                                  |
| --------------------- | ------------------------------------------------ |
| instance_names        | Names of the created VM instances.               |
| instance_ids          | Server-assigned unique identifiers of instances. |
| metadata_fingerprints | Unique fingerprints of the metadata.             |
| instance_self_links   | URIs of the created VM instances.                |
| tags_fingerprints     | Unique fingerprints of the tags.                 |
| label_fingerprints    | Unique fingerprints of the labels.               |
| cpu_platforms         | CPU platforms used by the instances.             |
| instance_statuses     | Current statuses of the instances.               |
| instance_count        | The value of the `instance_count` variable.      |

---
### ☁️ Tag Normalization Rules (GCP)

| Cloud | Case      | Allowed Characters | Example                            |
|--------|-----------|------------------|------------------------------------|
| **GCP** | TitleCase | Any              | `Name`, `Environment`, `CostCenter` |

---

### 💙 Maintained by [Vikas]
> Vikas — Simplifying Cloud, Securing Scale.