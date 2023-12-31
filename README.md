# amazon-eks

[![Linting](https://github.com/chadwickcloudservices/amazon-eks/actions/workflows/linting.yml/badge.svg)](https://github.com/chadwickcloudservices/amazon-eks/actions/workflows/linting.yml)
[![Deployment](https://github.com/chadwickcloudservices/amazon-eks/actions/workflows/deployment.yml/badge.svg)](https://github.com/chadwickcloudservices/amazon-eks/actions/workflows/deployment.yml)
[![License: Apache 2.0](https://img.shields.io/badge/License-Apache_2.0-purple.svg)](https://opensource.org/licenses/Apache-2.0)

Deploys Amazon EKS and dependent resources via GitHub Actions

### Assumptions

- You have permissions to deploy the referenced resources in your AWS account
- You have the version of Terraform and AWS CLI referenced in the [Requirements](https://github.com/chadwickcloudservices/amazon-eks#requirements) section

### Usage

1. "Create a new fork" of this repository
   1. NOTE: If you don't want to enable the scheduled workflow, ignore steps 2-6
2. Within your forked repo, navigate to the "Actions" settings
3. Select "I understand my workflows, go ahead and enable them"
4. Select "Enable workflow"
5. Select the "Linting" workflow on the left pane
6. Select "Run workflow" > "Run workflow"
   1. This will execute the "Linting" pipeline
7. Remaining steps will occur within your local development environment
8. [Establish AWS CLI authentication]
9. Clone your forked version of this repository and navigate to the root
10. Deploy resources by executing the deploy-tf.sh script with the '-p' flag
```bash
./deploy-tf.sh -p
```
11. deploy-tf.sh (extended functionality for informational purposes)
```bash
# 'p' flag is used to deploy resources to an aws account using GitHub Actions
./deploy-tf.sh -p

# 'p' and 'm' flags are used for doing the same as above, with a custom commit message
./deploy-tf.sh -p -m "This is my custom commit message"

# 'f' flag is exclusively used by GitHub Actions to execute scheduled linting
./deploy-tf.sh -f
```

### GitHub Actions CI/CD Pipeline (Expanded version)

![alt text](resources/GitHub%20Actions%20Pipeline.png)

### Amazon EKS Architecture (User facing workload example)

![alt text](resources/Amazon%20EKS%20Architecture.png)

### Amazon EKS Architecture (Cluster components)

![alt text](resources/Amazon%20EKS%20Architecture%20-%20Cluster%20Components.png)

### Requirements

| Name                                                                                     | Version  |
| -----------------------------------------------------------------------------------------|----------|
| [aws provider](https://registry.terraform.io/providers/hashicorp/aws/latest/docs)        | ~> 5.20  |
| [terraform](https://developer.hashicorp.com/terraform/downloads)                         | ~> 1.5.7 |
| [aws cli](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html) | ~> 2.7   |

### Resources

| Name                                                                                                                                                         | Type        |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------ | ----------- |
| [aws_secretsmanager_secret.key-pair](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/secretsmanager_secret)                      | resource    |
| [aws_secretsmanager_secret_version.key-pair](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/secretsmanager_secret_version)      | resource    |
| [aws_security_group.remote_access](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/security_group)                               | resource    |
| [aws_iam_policy.node_additional](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_policy)                                     | resource    |
| [aws_autoscaling_group_tag.cluster_autoscaler_label_tags](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/autoscaling_group_tag) | resource    |
| [aws_caller_identity.current](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/caller_identity)                                | data source |
| [aws_availability_zones.available](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/availability_zones)                        | data source |
| [aws_ami.eks_default](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/ami)                                                       | data source |

### External Modules

| Name                                                                              | Version    |
| ----------------------------------------------------------------------------------|------------|
| [eks](https://registry.terraform.io/modules/terraform-aws-modules/eks/aws/latest) | ~> 19.17.2 |

### References

 - [Amazon EKS]
 - [Kubernetes]
 - [GitHub Actions]
 - [Terraform EKS]

### License

© 2023 [Brian Chadwick](https://github.com/chadwickcloudservices)
Made available under the terms of the [Apache License 2.0].

[amazon eks]: https://docs.aws.amazon.com/eks/
[kubernetes]: https://kubernetes.io/docs/home/
[github actions]: https://docs.github.com/en/actions/quickstart
[terraform eks]: https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/eks_cluster
[establish aws cli authentication]: https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-authentication.html