<!-- This file was automatically generated by the `build-harness`. Make all changes to `README.yaml` and run `make readme` to rebuild this file. -->
[![README Header][readme_header_img]][readme_header_link]

[![Cloud Posse][logo]](https://cpco.io/homepage)

# terraform-aws-codefresh-backing-services

 [![Build Status](https://travis-ci.org/cloudposse/terraform-aws-codefresh-backing-services.svg?branch=master)](https://travis-ci.org/cloudposse/terraform-aws-codefresh-backing-services) [![Latest Release](https://img.shields.io/github/release/cloudposse/terraform-aws-codefresh-backing-services.svg)](https://github.com/cloudposse/terraform-aws-codefresh-backing-services/releases/latest) [![Slack Community](https://slack.cloudposse.com/badge.svg)](https://slack.cloudposse.com)


Terraform module to provision CodeFresh Enterprise backing services


---

This project is part of our comprehensive ["SweetOps"](https://cpco.io/sweetops) approach towards DevOps. 
[<img align="right" title="Share via Email" src="https://docs.cloudposse.com/images/ionicons/ios-email-outline-2.0.1-16x16-999999.svg"/>][share_email]
[<img align="right" title="Share on Google+" src="https://docs.cloudposse.com/images/ionicons/social-googleplus-outline-2.0.1-16x16-999999.svg" />][share_googleplus]
[<img align="right" title="Share on Facebook" src="https://docs.cloudposse.com/images/ionicons/social-facebook-outline-2.0.1-16x16-999999.svg" />][share_facebook]
[<img align="right" title="Share on Reddit" src="https://docs.cloudposse.com/images/ionicons/social-reddit-outline-2.0.1-16x16-999999.svg" />][share_reddit]
[<img align="right" title="Share on LinkedIn" src="https://docs.cloudposse.com/images/ionicons/social-linkedin-outline-2.0.1-16x16-999999.svg" />][share_linkedin]
[<img align="right" title="Share on Twitter" src="https://docs.cloudposse.com/images/ionicons/social-twitter-outline-2.0.1-16x16-999999.svg" />][share_twitter]


[![Terraform Open Source Modules](https://docs.cloudposse.com/images/terraform-open-source-modules.svg)][terraform_modules]



It's 100% Open Source and licensed under the [APACHE2](LICENSE).







We literally have [*hundreds of terraform modules*][terraform_modules] that are Open Source and well-maintained. Check them out! 






## Introduction

The module provisions the following resources:
- AWS Aurora cluster
- AWS Elasticache Redis
- AWS AmazonMQ (ActiveMQ)
- AWS S3 bucket with associated user and permissions
- AWS EFS

## Usage

```terraform
module "codefresh_backing_services" {
  source          = "git::https://github.com/cloudposse/terraform-aws-codefresh-backing-services.git?ref=master"
  enabled         = "true"
  name            = "${var.name}"
  namespace       = "${var.namespace}"
  region          = "${var.region}"
  stage           = "${var.stage}"
  vpc_id          = "${module.vpc.vpc_id}"
  subnet_ids      = ["${module.subnets.private_subnet_ids}"]
  security_groups = ["${module.vpc.vpc_default_security_group_id}"]
}
```

For a complete example, see [examples/complete](examples/complete)
TODO






## Makefile Targets
```
Available targets:

  help                                Help screen
  help/all                            Display help for all targets
  help/short                          This help short screen
  lint                                Lint terraform code

```

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|:----:|:-----:|:-----:|
| attributes | Additional attributes (e.g. `1`) | list | `<list>` | no |
| aws_assume_role_arn |  | string | - | yes |
| chamber_format | Format to store parameters in SSM, for consumption with chamber | string | `/%s/%s` | no |
| chamber_service | `chamber` service name. See [chamber usage](https://github.com/segmentio/chamber#usage) for more details | string | `` | no |
| delimiter | Delimiter to be used between `namespace`, `stage`, `name` and `attributes` | string | `-` | no |
| efs_enabled | Set to false to prevent the module from creating any resources | string | `` | no |
| enabled | Set to false to prevent the module from creating any resources | string | `true` | no |
| kms_key_id | KMS key id used to encrypt SSM parameters | string | `` | no |
| mq_apply_immediately | Specifies whether any cluster modifications are applied immediately, or during the next maintenance window | string | `true` | no |
| mq_audit_log | Enables audit logging. User management action made using JMX or the ActiveMQ Web Console is logged | string | `true` | no |
| mq_auto_minor_version_upgrade | Enables automatic upgrades to new minor versions for brokers, as Apache releases the versions | string | `false` | no |
| mq_deployment_mode | The deployment mode of the broker. Supported: SINGLE_INSTANCE and ACTIVE_STANDBY_MULTI_AZ | string | `ACTIVE_STANDBY_MULTI_AZ` | no |
| mq_enabled | Set to false to prevent the module from creating any resources | string | `` | no |
| mq_engine_type | The type of broker engine. Currently, Amazon MQ supports only ActiveMQ | string | `ActiveMQ` | no |
| mq_engine_version | The version of the broker engine. Currently, Amazon MQ supports only 5.15.0 or 5.15.6. | string | `5.15.0` | no |
| mq_general_log | Enables general logging via CloudWatch | string | `true` | no |
| mq_host_instance_type | The broker's instance type. e.g. mq.t2.micro or mq.m4.large | string | `mq.t2.micro` | no |
| mq_maintenance_day_of_week | The day of the week. e.g. MONDAY, TUESDAY, or WEDNESDAY | string | `SUNDAY` | no |
| mq_maintenance_time_of_day | The time, in 24-hour format. e.g. 02:00 | string | `03:00` | no |
| mq_maintenance_time_zone | The time zone, in either the Country/City format, or the UTC offset format. e.g. CET | string | `UTC` | no |
| mq_publicly_accessible | Whether to enable connections from applications outside of the VPC that hosts the broker's subnets. | string | `false` | no |
| name | Name  (e.g. `codefresh`) | string | `codefresh` | no |
| namespace | Namespace (e.g. `eg` or `cp`) | string | - | yes |
| overwrite_ssm_parameter | Whether to overwrite an existing SSM parameter | string | `true` | no |
| postgres_admin_password | Postgres password for the admin user | string | `` | no |
| postgres_admin_user | Postgres admin user name | string | `` | no |
| postgres_cluster_enabled | Set to false to prevent the module from creating any resources | string | `` | no |
| postgres_cluster_family | Postgres cluster DB family. Currently supported values are `aurora-postgresql9.6` and `aurora-postgresql10` | string | `aurora-postgresql9.6` | no |
| postgres_cluster_size | Postgres cluster size | string | `2` | no |
| postgres_db_name | Postgres database name | string | `` | no |
| postgres_instance_type | EC2 instance type for Postgres cluster | string | `db.r4.large` | no |
| postgres_maintenance_window | Weekly time range during which system maintenance can occur, in UTC | string | `sun:03:00-sun:04:00` | no |
| redis_apply_immediately | Whether to apply changes immediately or during the next maintenance_window | string | `true` | no |
| redis_at_rest_encryption_enabled | Enable Redis encryption at rest | string | `true` | no |
| redis_auth_token | Auth token for password protecting redis, transit_encryption_enabled must be set to 'true'! Password must be longer than 16 chars | string | `` | no |
| redis_automatic_failover | Whether to enable automatic_failover | string | `true` | no |
| redis_cluster_enabled | Set to false to prevent the module from creating any resources | string | `` | no |
| redis_cluster_size | Redis cluster size | string | `2` | no |
| redis_engine_version | Version of Redis engine | string | `3.2.6` | no |
| redis_instance_type | EC2 instance type for Redis cluster | string | `cache.t2.medium` | no |
| redis_maintenance_window | Weekly time range during which system maintenance can occur, in UTC | string | `sun:03:00-sun:04:00` | no |
| redis_params | A list of Redis parameters to apply. Note that parameters may differ from a Redis family to another | list | `<list>` | no |
| redis_transit_encryption_enabled | Enable TLS | string | `true` | no |
| s3_access_key_name | S3 user IAM access key name for storing in SSM. Default to aws_acces_key_id so chamber exports as AWS_ACCESS_KEY_ID, a standard AWS IAM ENV variable | string | `aws_access_key_id` | no |
| s3_allowed_bucket_actions | List of actions to permit for S3 bucket | list | `<list>` | no |
| s3_enabled | Set to false to prevent the module from creating any resources | string | `` | no |
| s3_secret_key_name | S3 user IAM secret key name for storing in SSM. Default to aws_secret_acces_key so chamber exports as AWS_SECRET_ACCESS_KEY, a standard AWS IAM ENV variable | string | `aws_secret_access_key` | no |
| s3_user_enabled | Set to `true` to create an S3 user with permission to access the bucket | string | `` | no |
| s3_versioning_enabled | Whether to enable versioning on the S3 bucket. | string | `false` | no |
| security_groups | List of security groups to be allowed to connect to the CodeFresh backing services | list | `<list>` | no |
| stage | Stage (e.g. `prod`, `dev`, `staging`) | string | - | yes |
| subnet_ids | A list of subnet IDs to launch the CodeFresh backing services in | list | `<list>` | no |
| tags | Additional tags (e.g. map(`Cluster`,`us-east-1.cloudposse.co`) | map | `<map>` | no |
| vpc_id | VPC ID for the CodeFresh backing services | string | - | yes |
| zone_name | DNS zone name | string | - | yes |

## Outputs

| Name | Description |
|------|-------------|
| aurora_postgres_cluster_name | Aurora Postgres Cluster Identifier |
| aurora_postgres_database_name | Aurora Postgres Database name |
| aurora_postgres_master_hostname | Aurora Postgres DB Master hostname |
| aurora_postgres_master_username | Aurora Postgres Username for the master DB user |
| aurora_postgres_replicas_hostname | Aurora Postgres Replicas hostname |
| efs_arn | EFS arn |
| efs_dns_name | EFS DNS name |
| efs_host | EFS host |
| efs_id | EFS ID |
| efs_mount_target_dns_names | EFS mount target DNS names |
| efs_mount_target_ids | EFS mount target IDs |
| efs_mount_target_ips | EFS mount target IPs |
| efs_network_interface_ids | EFS network interface IDs |
| elasticache_redis_host | Elasticache Redis host |
| elasticache_redis_id | Elasticache Redis cluster ID |
| elasticache_redis_security_group_id | Elasticache Redis security group ID |
| mq_admin_username | AmazonMQ admin username |
| mq_application_username | AmazonMQ application username |
| mq_broker_arn | AmazonMQ broker ARN |
| mq_broker_id | AmazonMQ broker ID |
| mq_primary_ampq_ssl_endpoint | AmazonMQ primary AMQP+SSL endpoint |
| mq_primary_console_url | AmazonMQ active web console URL |
| mq_primary_ip_address | AmazonMQ primary IP address |
| mq_secondary_ampq_ssl_endpoint | AmazonMQ secondary AMQP+SSL endpoint |
| mq_secondary_console_url | AmazonMQ secondary web console URL |
| mq_secondary_ip_address | AmazonMQ secondary IP address |
| s3_access_key_id | The access key ID |
| s3_bucket_arn | The s3 bucket ARN |
| s3_secret_access_key | The secret access key. This will be written to the state file in plain-text |
| s3_user_arn | The ARN assigned by AWS for the user |
| s3_user_name | Normalized IAM user name |
| s3_user_unique_id | The user unique ID assigned by AWS |




## Share the Love 

Like this project? Please give it a ★ on [our GitHub](https://github.com/cloudposse/terraform-aws-codefresh-backing-services)! (it helps us **a lot**) 

Are you using this project or any of our other projects? Consider [leaving a testimonial][testimonial]. =)


## Related Projects

Check out these related projects.

- [terraform-null-label](https://github.com/cloudposse/terraform-null-label) - Terraform Module to define a consistent naming convention by (namespace, stage, name, [attributes])
- [terraform-aws-rds-cluster](https://github.com/cloudposse/terraform-aws-rds-cluster) - Terraform module to provision an RDS Aurora cluster for MySQL or Postgres
- [terraform-aws-route53-cluster-hostname](https://github.com/cloudposse/terraform-aws-route53-cluster-hostname) - Terraform module to define a consistent AWS Route53 hostname
- [terraform-aws-kops-metadata](https://github.com/cloudposse/terraform-aws-kops-metadata) - Terraform module to lookup resources within a Kops cluster for easier integration with Terraform
- [terraform-aws-elasticache-redis](https://github.com/cloudposse/terraform-aws-elasticache-redis) - Terraform module to provision an ElastiCache Redis Cluster
- [terraform-aws-rds-cluster-instance-group](https://github.com/cloudposse/terraform-aws-rds-cluster-instance-group) - Terraform module to provision an RDS cluster instance pool with a dedicated endpoint
- [terraform-aws-vpc](https://github.com/cloudposse/terraform-aws-vpc) - Terraform Module that defines a VPC with public/private subnets across multiple AZs with Internet Gateways
- [terraform-aws-dynamic-subnets](https://github.com/cloudposse/terraform-aws-dynamic-subnets) - Terraform module for public and private subnets provisioning in existing VPC



## Help

**Got a question?**

File a GitHub [issue](https://github.com/cloudposse/terraform-aws-codefresh-backing-services/issues), send us an [email][email] or join our [Slack Community][slack].

[![README Commercial Support][readme_commercial_support_img]][readme_commercial_support_link]

## Commercial Support

Work directly with our team of DevOps experts via email, slack, and video conferencing. 

We provide [*commercial support*][commercial_support] for all of our [Open Source][github] projects. As a *Dedicated Support* customer, you have access to our team of subject matter experts at a fraction of the cost of a full-time engineer. 

[![E-Mail](https://img.shields.io/badge/email-hello@cloudposse.com-blue.svg)][email]

- **Questions.** We'll use a Shared Slack channel between your team and ours.
- **Troubleshooting.** We'll help you triage why things aren't working.
- **Code Reviews.** We'll review your Pull Requests and provide constructive feedback.
- **Bug Fixes.** We'll rapidly work to fix any bugs in our projects.
- **Build New Terraform Modules.** We'll [develop original modules][module_development] to provision infrastructure.
- **Cloud Architecture.** We'll assist with your cloud strategy and design.
- **Implementation.** We'll provide hands-on support to implement our reference architectures. 



## Terraform Module Development

Are you interested in custom Terraform module development? Submit your inquiry using [our form][module_development] today and we'll get back to you ASAP.


## Slack Community

Join our [Open Source Community][slack] on Slack. It's **FREE** for everyone! Our "SweetOps" community is where you get to talk with others who share a similar vision for how to rollout and manage infrastructure. This is the best place to talk shop, ask questions, solicit feedback, and work together as a community to build totally *sweet* infrastructure.

## Newsletter

Signup for [our newsletter][newsletter] that covers everything on our technology radar.  Receive updates on what we're up to on GitHub as well as awesome new projects we discover. 

## Contributing

### Bug Reports & Feature Requests

Please use the [issue tracker](https://github.com/cloudposse/terraform-aws-codefresh-backing-services/issues) to report any bugs or file feature requests.

### Developing

If you are interested in being a contributor and want to get involved in developing this project or [help out](https://cpco.io/help-out) with our other projects, we would love to hear from you! Shoot us an [email][email].

In general, PRs are welcome. We follow the typical "fork-and-pull" Git workflow.

 1. **Fork** the repo on GitHub
 2. **Clone** the project to your own machine
 3. **Commit** changes to your own branch
 4. **Push** your work back up to your fork
 5. Submit a **Pull Request** so that we can review your changes

**NOTE:** Be sure to merge the latest changes from "upstream" before making a pull request!


## Copyright

Copyright © 2017-2019 [Cloud Posse, LLC](https://cpco.io/copyright)



## License 

[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0) 

See [LICENSE](LICENSE) for full details.

    Licensed to the Apache Software Foundation (ASF) under one
    or more contributor license agreements.  See the NOTICE file
    distributed with this work for additional information
    regarding copyright ownership.  The ASF licenses this file
    to you under the Apache License, Version 2.0 (the
    "License"); you may not use this file except in compliance
    with the License.  You may obtain a copy of the License at

      https://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing,
    software distributed under the License is distributed on an
    "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
    KIND, either express or implied.  See the License for the
    specific language governing permissions and limitations
    under the License.









## Trademarks

All other trademarks referenced herein are the property of their respective owners.

## About

This project is maintained and funded by [Cloud Posse, LLC][website]. Like it? Please let us know by [leaving a testimonial][testimonial]!

[![Cloud Posse][logo]][website]

We're a [DevOps Professional Services][hire] company based in Los Angeles, CA. We ❤️  [Open Source Software][we_love_open_source].

We offer [paid support][commercial_support] on all of our projects.  

Check out [our other projects][github], [follow us on twitter][twitter], [apply for a job][jobs], or [hire us][hire] to help with your cloud strategy and implementation.



### Contributors

|  [![Erik Osterman][osterman_avatar]][osterman_homepage]<br/>[Erik Osterman][osterman_homepage] | [![Andriy Knysh][aknysh_avatar]][aknysh_homepage]<br/>[Andriy Knysh][aknysh_homepage] | [![Igor Rodionov][goruha_avatar]][goruha_homepage]<br/>[Igor Rodionov][goruha_homepage] | [![Josh Myers][joshmyers_avatar]][joshmyers_homepage]<br/>[Josh Myers][joshmyers_homepage] |
|---|---|---|---|


  [osterman_homepage]: https://github.com/osterman
  [osterman_avatar]: http://s.gravatar.com/avatar/88c480d4f73b813904e00a5695a454cb?s=144


  [aknysh_homepage]: https://github.com/aknysh/
  [aknysh_avatar]: https://avatars0.githubusercontent.com/u/7356997?v=4&u=ed9ce1c9151d552d985bdf5546772e14ef7ab617&s=144


  [goruha_homepage]: https://github.com/goruha/
  [goruha_avatar]: http://s.gravatar.com/avatar/bc70834d32ed4517568a1feb0b9be7e2?s=144

  [joshmyers_homepage]: https://github.com/joshmyers
  [joshmyers_avatar]: https://github.com/joshmyers.png?size=150



[![README Footer][readme_footer_img]][readme_footer_link]
[![Beacon][beacon]][website]

  [logo]: https://cloudposse.com/logo-300x69.svg
  [docs]: https://cpco.io/docs
  [website]: https://cpco.io/homepage
  [github]: https://cpco.io/github
  [jobs]: https://cpco.io/jobs
  [hire]: https://cpco.io/hire
  [slack]: https://cpco.io/slack
  [linkedin]: https://cpco.io/linkedin
  [twitter]: https://cpco.io/twitter
  [testimonial]: https://cpco.io/leave-testimonial
  [newsletter]: https://cpco.io/newsletter
  [email]: https://cpco.io/email
  [commercial_support]: https://cpco.io/commercial-support
  [we_love_open_source]: https://cpco.io/we-love-open-source
  [module_development]: https://cpco.io/module-development
  [terraform_modules]: https://cpco.io/terraform-modules
  [readme_header_img]: https://cloudposse.com/readme/header/img?repo=cloudposse/terraform-aws-codefresh-backing-services
  [readme_header_link]: https://cloudposse.com/readme/header/link?repo=cloudposse/terraform-aws-codefresh-backing-services
  [readme_footer_img]: https://cloudposse.com/readme/footer/img?repo=cloudposse/terraform-aws-codefresh-backing-services
  [readme_footer_link]: https://cloudposse.com/readme/footer/link?repo=cloudposse/terraform-aws-codefresh-backing-services
  [readme_commercial_support_img]: https://cloudposse.com/readme/commercial-support/img?repo=cloudposse/terraform-aws-codefresh-backing-services
  [readme_commercial_support_link]: https://cloudposse.com/readme/commercial-support/link?repo=cloudposse/terraform-aws-codefresh-backing-services
  [share_twitter]: https://twitter.com/intent/tweet/?text=terraform-aws-codefresh-backing-services&url=https://github.com/cloudposse/terraform-aws-codefresh-backing-services
  [share_linkedin]: https://www.linkedin.com/shareArticle?mini=true&title=terraform-aws-codefresh-backing-services&url=https://github.com/cloudposse/terraform-aws-codefresh-backing-services
  [share_reddit]: https://reddit.com/submit/?url=https://github.com/cloudposse/terraform-aws-codefresh-backing-services
  [share_facebook]: https://facebook.com/sharer/sharer.php?u=https://github.com/cloudposse/terraform-aws-codefresh-backing-services
  [share_googleplus]: https://plus.google.com/share?url=https://github.com/cloudposse/terraform-aws-codefresh-backing-services
  [share_email]: mailto:?subject=terraform-aws-codefresh-backing-services&body=https://github.com/cloudposse/terraform-aws-codefresh-backing-services
  [beacon]: https://ga-beacon.cloudposse.com/UA-76589703-4/cloudposse/terraform-aws-codefresh-backing-services?pixel&cs=github&cm=readme&an=terraform-aws-codefresh-backing-services
