# 🏗️ Terraform-google-vm
# Google Cloud Infrastructure Provisioning with Terraform

[![OpsStation](https://img.shields.io/badge/Made%20by-OpsStation-blue?style=flat-square&logo=terraform)](https://www.opsstation.com)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Terraform](https://img.shields.io/badge/Terraform-1.13%2B-purple.svg?logo=terraform)](#)
[![CI](https://github.com/OpsStation/terraform-gcp-vm/actions/workflows/ci.yml/badge.svg)](https://github.com/OpsStation/terraform-gcp-vm/actions/workflows/ci.yml)
[![Latest Release](https://img.shields.io/github/release/opsstation/terraform-gcp-vm.svg)](https://github.com/opsstation/terraform-gcp-vm/releases/latest)

> 🌩️ **A production-grade, reusable GCP vm module by [OpsStation](https://www.opsstation.com)**
> Designed for reliability, performance, and security — following GCP networking best practices.
---

## 🏢 About OpsStation

**OpsStation** delivers **Cloud & DevOps excellence** for modern teams:
- 🚀 **Infrastructure Automation** with Terraform, Ansible & Kubernetes
- 💰 **Cost Optimization** via scaling & right-sizing
- 🛡️ **Security & Compliance** baked into CI/CD pipelines
- ⚙️ **Fully Managed Operations** across GCP, Azure, and AWS

> 💡 Need enterprise-grade DevOps automation?
> 👉 Visit [**www.opsstation.com**](https://www.opsstation.com) or email **hello@opsstation.com**

---
## 🌟 Features

🔥 Terraform GCP VM Instance Module – Key Features

- ✅ Create highly configurable GCP VM instances with full support for machine type, zone, custom hostname, and metadata

- ✅ Seamless label management using the OpsStation Multicloud Labels Module
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
      source                 = "opsstation/vm/gcp"
      version                = "1.0.1"
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

### 💙 Maintained by [OpsStation](https://www.opsstation.com)
> OpsStation — Simplifying Cloud, Securing Scale.