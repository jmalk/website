---
title: Terraform
tags: learning
---
# Terraform

## Why?

Control infrastructure as code rather than clicking around in a GUI.

## How?

- Write a config like `main.tf`.
- Run `terraform init` to download any providers (plugins that let terraform interact with other apps or services) your config depends on.
- Run `terraform plan` to see what will happen when you use the config.
- Run `terraform apply` to make the stuff happen.
- Run `terraform destroy` to stop it.
