---
layout: post
title: "IaC tools and platforms"
date: 2024-08-22 15:00:00 +0800
categories: []
---

This is a space that you would be extremely familiar with if you have infrastructure as code practices in your company

#### IaC Platforms

###### Terraform

Probably the most well-known out of the bunch. It has long history in this space

##### OpenTofu

You will also know this, if you know terraform and the controversy around how Terraform is no longer open source, and the community decided to create a separate fork that is still open source

##### Pulumi

Coined as a terraform alternative, the advantage being that you are writing it in programming languages such as typescript, which in theory provides more flexibility in what can be done

##### AWS CloudFormation

AWS native. I have used it in limited extent and scope, however I have not heard good things about it, and since it is AWS only, it only makes sense to be here if everything you run is AWS native, which in my experience is never the case. Eg. your DNS servers might be in CloudFlare, you use GitHub instead of AWS CodeCommit. Or you have a multi-cloud strategy which you deploy across multiple clouds: AWS, GCP, Azure

##### Azure Resource Manager/Bicep

Azure native. Again, only used it in limited scope. Likely same limitations as CloudFormation

##### Crossplane

This one is very interesting, give it utilizes k8s CRDs to maintain infrastructural resources. Personally I do not see this used from a IT/CloudOps perspective, but I can really see this being used in companies that:
1. Has multiple teams, and frequently creates new infrastructure to be utilized in kubernetes. For example, creating a kubernetes deployment, bundled with a AWS managed PostgreSQL DB for testing. By incorporating/bundling the AWS managed PostgreSQL DB into a helm chart, deployment of a full end to end application can be dead simple and quick
2. If you have some sort of multi-tenant, multi-instance app deployment strategy (see [KubePlus](https://github.com/cloud-ark/kubeplus?tab=readme-ov-file#kubeplus---kubernetes-operator-for-multi-instance-multi-tenancy)). Similarly, you can achieve simple end to end deployment just by using helm charts alone

##### Ansible

This is technically still code/scripts. I'd thought this would be a worthy mention. It primarily focuses on configuring provisioned/deployed instances, though nowadays I would probably utilize either docker, or something like packer to create immutable images. The other key difference is also that this isn't declarative but imperative, which really shows you the shift in paradigm on how we think about provisioning infrastructure in the present, vs the past

#### IaC Tools

##### Terragrunt

This focuses on enriching the terraform experience and covering the DRY aspects of maintaining terraform as much as possible, given its shortcomings around this department

##### SpaceLift/Scalr/Env0/Atlantis

This is primarily "CI/CD" type platforms to maintain our IaC codes in a more process oriented manner

