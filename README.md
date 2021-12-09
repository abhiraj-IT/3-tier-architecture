# 3-tier-vpc

All Logs to verify..

Admin@DevOps MINGW64 ~/Desktop/test/3-tier-architecture (main)
$ terraform init
Initializing modules...
- autoscaling in modules\autoscaling
Downloading terraform-aws-modules/alb/aws 5.16.0 for autoscaling.alb...
- autoscaling.alb in .terraform\modules\autoscaling.alb
Downloading terraform-in-action/iip/aws 0.1.0 for autoscaling.iam_instance_profile...
- autoscaling.iam_instance_profile in .terraform\modules\autoscaling.iam_instance_profile
- database in modules\database
- networking in modules\networking
Downloading terraform-in-action/sg/aws 0.1.0 for networking.db_sg...
- networking.db_sg in .terraform\modules\networking.db_sg
Downloading terraform-in-action/sg/aws 0.1.0 for networking.lb_sg...
- networking.lb_sg in .terraform\modules\networking.lb_sg
Downloading terraform-aws-modules/vpc/aws 2.64.0 for networking.vpc...
- networking.vpc in .terraform\modules\networking.vpc
Downloading terraform-in-action/sg/aws 0.1.0 for networking.websvr_sg...
- networking.websvr_sg in .terraform\modules\networking.websvr_sg

Initializing the backend...

Initializing provider plugins...
- Reusing previous version of hashicorp/aws from the dependency lock file
- Reusing previous version of hashicorp/cloudinit from the dependency lock file
- Reusing previous version of hashicorp/random from the dependency lock file
- Installing hashicorp/cloudinit v2.2.0...
- Installed hashicorp/cloudinit v2.2.0 (signed by HashiCorp)
- Installing hashicorp/random v3.1.0...
- Installed hashicorp/random v3.1.0 (signed by HashiCorp)
- Installing hashicorp/aws v3.63.0...
- Installed hashicorp/aws v3.63.0 (signed by HashiCorp)

Terraform has made some changes to the provider dependency selections recorded
in the .terraform.lock.hcl file. Review those changes and commit them to your
version control system if they represent changes you intended to make.

Terraform has been successfully initialized!

You may now begin working with Terraform. Try running "terraform plan" to see
any changes that are required for your infrastructure. All Terraform commands
should now work.

If you ever set or change modules or backend configuration for Terraform,
rerun this command to reinitialize your working directory. If you forget, other
commands will detect it and remind you to do so if necessary.

Admin@DevOps MINGW64 ~/Desktop/test/3-tier-architecture (main)
$ terraform plan

Terraform used the selected providers to generate the following execution
plan. Resource actions are indicated with the following symbols:
  + create
 <= read (data resources)

Terraform will perform the following actions:

  # module.autoscaling.data.cloudinit_config.config will be read during apply
  # (config refers to values not yet known)
 <= data "cloudinit_config" "config"  {
      + base64_encode = true
      + gzip          = true
      + id            = (known after apply)
      + rendered      = (known after apply)

      + part {
          + content      = (sensitive)
          + content_type = "text/cloud-config"
        }
    }

  # module.autoscaling.aws_autoscaling_group.webserver will be created
  + resource "aws_autoscaling_group" "webserver" {
      + arn                       = (known after apply)
      + availability_zones        = (known after apply)
      + default_cooldown          = (known after apply)
      + desired_capacity          = (known after apply)
      + force_delete              = false
      + force_delete_warm_pool    = false
      + health_check_grace_period = 300
      + health_check_type         = (known after apply)
      + id                        = (known after apply)
      + max_size                  = 3
      + metrics_granularity       = "1Minute"
      + min_size                  = 1
      + name                      = "my-3-tier-architecture-asg"
      + name_prefix               = (known after apply)
      + protect_from_scale_in     = false
      + service_linked_role_arn   = (known after apply)
      + target_group_arns         = (known after apply)
      + vpc_zone_identifier       = (known after apply)
      + wait_for_capacity_timeout = "10m"

      + launch_template {
          + id      = (known after apply)
          + name    = (known after apply)
          + version = (known after apply)
        }
    }

  # module.autoscaling.aws_launch_template.webserver will be created
  + resource "aws_launch_template" "webserver" {
      + arn                    = (known after apply)
      + default_version        = (known after apply)
      + id                     = (known after apply)
      + image_id               = "ami-074251216af698218"
      + instance_type          = "t2.micro"
      + latest_version         = (known after apply)
      + name                   = (known after apply)
      + name_prefix            = "my-3-tier-architecture"
      + tags_all               = (known after apply)
      + user_data              = (known after apply)
      + vpc_security_group_ids = (known after apply)

      + iam_instance_profile {
          + name = (known after apply)
        }

      + metadata_options {
          + http_endpoint               = (known after apply)
          + http_protocol_ipv6          = (known after apply)
          + http_put_response_hop_limit = (known after apply)
          + http_tokens                 = (known after apply)
        }
    }

  # module.database.aws_db_instance.database will be created
  + resource "aws_db_instance" "database" {
      + address                               = (known after apply)
      + allocated_storage                     = 10
      + apply_immediately                     = (known after apply)
      + arn                                   = (known after apply)
      + auto_minor_version_upgrade            = true
      + availability_zone                     = (known after apply)
      + backup_retention_period               = (known after apply)
      + backup_window                         = (known after apply)
      + ca_cert_identifier                    = (known after apply)
      + character_set_name                    = (known after apply)
      + copy_tags_to_snapshot                 = false
      + db_subnet_group_name                  = (known after apply)
      + delete_automated_backups              = true
      + endpoint                              = (known after apply)
      + engine                                = "mysql"
      + engine_version                        = "8.0"
      + engine_version_actual                 = (known after apply)
      + hosted_zone_id                        = (known after apply)
      + id                                    = (known after apply)
      + identifier                            = "my-3-tier-architecture-db-instance"
      + identifier_prefix                     = (known after apply)
      + instance_class                        = "db.t2.micro"
      + kms_key_id                            = (known after apply)
      + latest_restorable_time                = (known after apply)
      + license_model                         = (known after apply)
      + maintenance_window                    = (known after apply)
      + monitoring_interval                   = 0
      + monitoring_role_arn                   = (known after apply)
      + multi_az                              = (known after apply)
      + name                                  = "pets"
      + nchar_character_set_name              = (known after apply)
      + option_group_name                     = (known after apply)
      + parameter_group_name                  = (known after apply)
      + password                              = (sensitive value)
      + performance_insights_enabled          = false
      + performance_insights_kms_key_id       = (known after apply)
      + performance_insights_retention_period = (known after apply)
      + port                                  = (known after apply)
      + publicly_accessible                   = false
      + replicas                              = (known after apply)
      + resource_id                           = (known after apply)
      + skip_final_snapshot                   = true
      + snapshot_identifier                   = (known after apply)
      + status                                = (known after apply)
      + storage_type                          = (known after apply)
      + tags_all                              = (known after apply)
      + timezone                              = (known after apply)
      + username                              = "admin"
      + vpc_security_group_ids                = (known after apply)
    }

  # module.database.random_password.password will be created
  + resource "random_password" "password" {
      + id               = (known after apply)
      + length           = 16
      + lower            = true
      + min_lower        = 0
      + min_numeric      = 0
      + min_special      = 0
      + min_upper        = 0
      + number           = true
      + override_special = "_%@/'\""
      + result           = (sensitive value)
      + special          = true
      + upper            = true
    }

  # module.autoscaling.module.alb.aws_lb.this[0] will be created
  + resource "aws_lb" "this" {
      + arn                        = (known after apply)
      + arn_suffix                 = (known after apply)
      + dns_name                   = (known after apply)
      + drop_invalid_header_fields = false
      + enable_deletion_protection = false
      + enable_http2               = true
      + id                         = (known after apply)
      + idle_timeout               = 60
      + internal                   = false
      + ip_address_type            = "ipv4"
      + load_balancer_type         = "application"
      + name                       = "my-3-tier-architecture"
      + security_groups            = (known after apply)
      + subnets                    = (known after apply)
      + tags                       = {
          + "Name" = "my-3-tier-architecture"
        }
      + tags_all                   = {
          + "Name" = "my-3-tier-architecture"
        }
      + vpc_id                     = (known after apply)
      + zone_id                    = (known after apply)

      + subnet_mapping {
          + allocation_id        = (known after apply)
          + ipv6_address         = (known after apply)
          + outpost_id           = (known after apply)
          + private_ipv4_address = (known after apply)
          + subnet_id            = (known after apply)
        }

      + timeouts {
          + create = "10m"
          + delete = "10m"
          + update = "10m"
        }
    }

  # module.autoscaling.module.alb.aws_lb_listener.frontend_http_tcp[0] will be created
  + resource "aws_lb_listener" "frontend_http_tcp" {
      + arn               = (known after apply)
      + id                = (known after apply)
      + load_balancer_arn = (known after apply)
      + port              = 80
      + protocol          = "HTTP"
      + ssl_policy        = (known after apply)
      + tags_all          = (known after apply)

      + default_action {
          + order            = (known after apply)
          + target_group_arn = (known after apply)
          + type             = "forward"
        }
    }

  # module.autoscaling.module.alb.aws_lb_target_group.main[0] will be created
  + resource "aws_lb_target_group" "main" {
      + arn                                = (known after apply)
      + arn_suffix                         = (known after apply)
      + deregistration_delay               = "300"
      + id                                 = (known after apply)
      + lambda_multi_value_headers_enabled = false
      + load_balancing_algorithm_type      = (known after apply)
      + name                               = (known after apply)
      + name_prefix                        = "websvr"
      + port                               = 8080
      + preserve_client_ip                 = (known after apply)
      + protocol                           = "HTTP"
      + protocol_version                   = (known after apply)
      + proxy_protocol_v2                  = false
      + slow_start                         = 0
      + tags                               = {
          + "Name" = "websvr"
        }
      + tags_all                           = {
          + "Name" = "websvr"
        }
      + target_type                        = "instance"
      + vpc_id                             = (known after apply)

      + health_check {
          + enabled             = (known after apply)
          + healthy_threshold   = (known after apply)
          + interval            = (known after apply)
          + matcher             = (known after apply)
          + path                = (known after apply)
          + port                = (known after apply)
          + protocol            = (known after apply)
          + timeout             = (known after apply)
          + unhealthy_threshold = (known after apply)
        }

      + stickiness {
          + cookie_duration = (known after apply)
          + cookie_name     = (known after apply)
          + enabled         = (known after apply)
          + type            = (known after apply)
        }
    }

  # module.autoscaling.module.iam_instance_profile.aws_iam_instance_profile.iam_instance_profile will be created
  + resource "aws_iam_instance_profile" "iam_instance_profile" {
      + arn         = (known after apply)
      + create_date = (known after apply)
      + id          = (known after apply)
      + name        = (known after apply)
      + path        = "/"
      + role        = (known after apply)
      + tags_all    = (known after apply)
      + unique_id   = (known after apply)
    }

  # module.autoscaling.module.iam_instance_profile.aws_iam_role.iam_role will be created
  + resource "aws_iam_role" "iam_role" {
      + arn                   = (known after apply)
      + assume_role_policy    = jsonencode(
            {
              + Statement = [
                  + {
                      + Action    = "sts:AssumeRole"
                      + Effect    = "Allow"
                      + Principal = {
                          + Service = "ec2.amazonaws.com"
                        }
                    },
                ]
              + Version   = "2012-10-17"
            }
        )
      + create_date           = (known after apply)
      + force_detach_policies = false
      + id                    = (known after apply)
      + managed_policy_arns   = (known after apply)
      + max_session_duration  = 3600
      + name                  = (known after apply)
      + name_prefix           = (known after apply)
      + path                  = "/"
      + tags_all              = (known after apply)
      + unique_id             = (known after apply)

      + inline_policy {
          + name   = (known after apply)
          + policy = (known after apply)
        }
    }

  # module.autoscaling.module.iam_instance_profile.aws_iam_role_policy.iam_role_policy will be created
  + resource "aws_iam_role_policy" "iam_role_policy" {
      + id     = (known after apply)
      + name   = (known after apply)
      + policy = jsonencode(
            {
              + Statement = [
                  + {
                      + Action   = [
                          + "rds:*",
                          + "logs:*",
                        ]
                      + Effect   = "Allow"
                      + Resource = "*"
                      + Sid      = ""
                    },
                ]
              + Version   = "2012-10-17"
            }
        )
      + role   = (known after apply)
    }

  # module.networking.module.db_sg.aws_security_group.security_group will be created
  + resource "aws_security_group" "security_group" {
      + arn                    = (known after apply)
      + description            = "Managed by Terraform"
      + egress                 = [
          + {
              + cidr_blocks      = [
                  + "0.0.0.0/0",
                ]
              + description      = ""
              + from_port        = 0
              + ipv6_cidr_blocks = []
              + prefix_list_ids  = []
              + protocol         = "-1"
              + security_groups  = []
              + self             = false
              + to_port          = 0
            },
        ]
      + id                     = (known after apply)
      + ingress                = [
          + {
              + cidr_blocks      = []
              + description      = ""
              + from_port        = 0
              + ipv6_cidr_blocks = []
              + prefix_list_ids  = []
              + protocol         = "-1"
              + security_groups  = []
              + self             = true
              + to_port          = 0
            },
          + {
              + cidr_blocks      = []
              + description      = ""
              + from_port        = 3306
              + ipv6_cidr_blocks = []
              + prefix_list_ids  = []
              + protocol         = "tcp"
              + security_groups  = (known after apply)
              + self             = false
              + to_port          = 3306
            },
        ]
      + name                   = (known after apply)
      + name_prefix            = (known after apply)
      + owner_id               = (known after apply)
      + revoke_rules_on_delete = false
      + tags_all               = (known after apply)
      + vpc_id                 = (known after apply)
    }

  # module.networking.module.lb_sg.aws_security_group.security_group will be created
  + resource "aws_security_group" "security_group" {
      + arn                    = (known after apply)
      + description            = "Managed by Terraform"
      + egress                 = [
          + {
              + cidr_blocks      = [
                  + "0.0.0.0/0",
                ]
              + description      = ""
              + from_port        = 0
              + ipv6_cidr_blocks = []
              + prefix_list_ids  = []
              + protocol         = "-1"
              + security_groups  = []
              + self             = false
              + to_port          = 0
            },
        ]
      + id                     = (known after apply)
      + ingress                = [
          + {
              + cidr_blocks      = [
                  + "0.0.0.0/0",
                ]
              + description      = ""
              + from_port        = 80
              + ipv6_cidr_blocks = []
              + prefix_list_ids  = []
              + protocol         = "tcp"
              + security_groups  = []
              + self             = false
              + to_port          = 80
            },
          + {
              + cidr_blocks      = []
              + description      = ""
              + from_port        = 0
              + ipv6_cidr_blocks = []
              + prefix_list_ids  = []
              + protocol         = "-1"
              + security_groups  = []
              + self             = true
              + to_port          = 0
            },
        ]
      + name                   = (known after apply)
      + name_prefix            = (known after apply)
      + owner_id               = (known after apply)
      + revoke_rules_on_delete = false
      + tags_all               = (known after apply)
      + vpc_id                 = (known after apply)
    }

  # module.networking.module.vpc.aws_db_subnet_group.database[0] will be created
  + resource "aws_db_subnet_group" "database" {
      + arn         = (known after apply)
      + description = "Database subnet group for my-3-tier-architecture-vpc"
      + id          = (known after apply)
      + name        = "my-3-tier-architecture-vpc"
      + name_prefix = (known after apply)
      + subnet_ids  = (known after apply)
      + tags        = {
          + "Name" = "my-3-tier-architecture-vpc"
        }
      + tags_all    = {
          + "Name" = "my-3-tier-architecture-vpc"
        }
    }

  # module.networking.module.vpc.aws_eip.nat[0] will be created
  + resource "aws_eip" "nat" {
      + allocation_id        = (known after apply)
      + association_id       = (known after apply)
      + carrier_ip           = (known after apply)
      + customer_owned_ip    = (known after apply)
      + domain               = (known after apply)
      + id                   = (known after apply)
      + instance             = (known after apply)
      + network_border_group = (known after apply)
      + network_interface    = (known after apply)
      + private_dns          = (known after apply)
      + private_ip           = (known after apply)
      + public_dns           = (known after apply)
      + public_ip            = (known after apply)
      + public_ipv4_pool     = (known after apply)
      + tags                 = {
          + "Name" = "my-3-tier-architecture-vpc-us-west-2a"
        }
      + tags_all             = {
          + "Name" = "my-3-tier-architecture-vpc-us-west-2a"
        }
      + vpc                  = true
    }

  # module.networking.module.vpc.aws_internet_gateway.this[0] will be created
  + resource "aws_internet_gateway" "this" {
      + arn      = (known after apply)
      + id       = (known after apply)
      + owner_id = (known after apply)
      + tags     = {
          + "Name" = "my-3-tier-architecture-vpc"
        }
      + tags_all = {
          + "Name" = "my-3-tier-architecture-vpc"
        }
      + vpc_id   = (known after apply)
    }

  # module.networking.module.vpc.aws_nat_gateway.this[0] will be created
  + resource "aws_nat_gateway" "this" {
      + allocation_id        = (known after apply)
      + connectivity_type    = "public"
      + id                   = (known after apply)
      + network_interface_id = (known after apply)
      + private_ip           = (known after apply)
      + public_ip            = (known after apply)
      + subnet_id            = (known after apply)
      + tags                 = {
          + "Name" = "my-3-tier-architecture-vpc-us-west-2a"
        }
      + tags_all             = {
          + "Name" = "my-3-tier-architecture-vpc-us-west-2a"
        }
    }

  # module.networking.module.vpc.aws_route.private_nat_gateway[0] will be created
  + resource "aws_route" "private_nat_gateway" {
      + destination_cidr_block = "0.0.0.0/0"
      + id                     = (known after apply)
      + instance_id            = (known after apply)
      + instance_owner_id      = (known after apply)
      + nat_gateway_id         = (known after apply)
      + network_interface_id   = (known after apply)
      + origin                 = (known after apply)
      + route_table_id         = (known after apply)
      + state                  = (known after apply)

      + timeouts {
          + create = "5m"
        }
    }

  # module.networking.module.vpc.aws_route.public_internet_gateway[0] will be created
  + resource "aws_route" "public_internet_gateway" {
      + destination_cidr_block = "0.0.0.0/0"
      + gateway_id             = (known after apply)
      + id                     = (known after apply)
      + instance_id            = (known after apply)
      + instance_owner_id      = (known after apply)
      + network_interface_id   = (known after apply)
      + origin                 = (known after apply)
      + route_table_id         = (known after apply)
      + state                  = (known after apply)

      + timeouts {
          + create = "5m"
        }
    }

  # module.networking.module.vpc.aws_route_table.private[0] will be created
  + resource "aws_route_table" "private" {
      + arn              = (known after apply)
      + id               = (known after apply)
      + owner_id         = (known after apply)
      + propagating_vgws = (known after apply)
      + route            = (known after apply)
      + tags             = {
          + "Name" = "my-3-tier-architecture-vpc-private"
        }
      + tags_all         = {
          + "Name" = "my-3-tier-architecture-vpc-private"
        }
      + vpc_id           = (known after apply)
    }

  # module.networking.module.vpc.aws_route_table.public[0] will be created
  + resource "aws_route_table" "public" {
      + arn              = (known after apply)
      + id               = (known after apply)
      + owner_id         = (known after apply)
      + propagating_vgws = (known after apply)
      + route            = (known after apply)
      + tags             = {
          + "Name" = "my-3-tier-architecture-vpc-public"
        }
      + tags_all         = {
          + "Name" = "my-3-tier-architecture-vpc-public"
        }
      + vpc_id           = (known after apply)
    }

  # module.networking.module.vpc.aws_route_table_association.database[0] will be created
  + resource "aws_route_table_association" "database" {
      + id             = (known after apply)
      + route_table_id = (known after apply)
      + subnet_id      = (known after apply)
    }

  # module.networking.module.vpc.aws_route_table_association.database[1] will be created
  + resource "aws_route_table_association" "database" {
      + id             = (known after apply)
      + route_table_id = (known after apply)
      + subnet_id      = (known after apply)
    }

  # module.networking.module.vpc.aws_route_table_association.database[2] will be created
  + resource "aws_route_table_association" "database" {
      + id             = (known after apply)
      + route_table_id = (known after apply)
      + subnet_id      = (known after apply)
    }

  # module.networking.module.vpc.aws_route_table_association.private[0] will be created
  + resource "aws_route_table_association" "private" {
      + id             = (known after apply)
      + route_table_id = (known after apply)
      + subnet_id      = (known after apply)
    }

  # module.networking.module.vpc.aws_route_table_association.private[1] will be created
  + resource "aws_route_table_association" "private" {
      + id             = (known after apply)
      + route_table_id = (known after apply)
      + subnet_id      = (known after apply)
    }

  # module.networking.module.vpc.aws_route_table_association.private[2] will be created
  + resource "aws_route_table_association" "private" {
      + id             = (known after apply)
      + route_table_id = (known after apply)
      + subnet_id      = (known after apply)
    }

  # module.networking.module.vpc.aws_route_table_association.public[0] will be created
  + resource "aws_route_table_association" "public" {
      + id             = (known after apply)
      + route_table_id = (known after apply)
      + subnet_id      = (known after apply)
    }

  # module.networking.module.vpc.aws_route_table_association.public[1] will be created
  + resource "aws_route_table_association" "public" {
      + id             = (known after apply)
      + route_table_id = (known after apply)
      + subnet_id      = (known after apply)
    }

  # module.networking.module.vpc.aws_route_table_association.public[2] will be created
  + resource "aws_route_table_association" "public" {
      + id             = (known after apply)
      + route_table_id = (known after apply)
      + subnet_id      = (known after apply)
    }

  # module.networking.module.vpc.aws_subnet.database[0] will be created
  + resource "aws_subnet" "database" {
      + arn                             = (known after apply)
      + assign_ipv6_address_on_creation = false
      + availability_zone               = "us-west-2a"
      + availability_zone_id            = (known after apply)
      + cidr_block                      = "10.0.21.0/24"
      + id                              = (known after apply)
      + ipv6_cidr_block_association_id  = (known after apply)
      + map_public_ip_on_launch         = false
      + owner_id                        = (known after apply)
      + tags                            = {
          + "Name" = "my-3-tier-architecture-vpc-db-us-west-2a"
        }
      + tags_all                        = {
          + "Name" = "my-3-tier-architecture-vpc-db-us-west-2a"
        }
      + vpc_id                          = (known after apply)
    }

  # module.networking.module.vpc.aws_subnet.database[1] will be created
  + resource "aws_subnet" "database" {
      + arn                             = (known after apply)
      + assign_ipv6_address_on_creation = false
      + availability_zone               = "us-west-2b"
      + availability_zone_id            = (known after apply)
      + cidr_block                      = "10.0.22.0/24"
      + id                              = (known after apply)
      + ipv6_cidr_block_association_id  = (known after apply)
      + map_public_ip_on_launch         = false
      + owner_id                        = (known after apply)
      + tags                            = {
          + "Name" = "my-3-tier-architecture-vpc-db-us-west-2b"
        }
      + tags_all                        = {
          + "Name" = "my-3-tier-architecture-vpc-db-us-west-2b"
        }
      + vpc_id                          = (known after apply)
    }

  # module.networking.module.vpc.aws_subnet.database[2] will be created
  + resource "aws_subnet" "database" {
      + arn                             = (known after apply)
      + assign_ipv6_address_on_creation = false
      + availability_zone               = "us-west-2c"
      + availability_zone_id            = (known after apply)
      + cidr_block                      = "10.0.23.0/24"
      + id                              = (known after apply)
      + ipv6_cidr_block_association_id  = (known after apply)
      + map_public_ip_on_launch         = false
      + owner_id                        = (known after apply)
      + tags                            = {
          + "Name" = "my-3-tier-architecture-vpc-db-us-west-2c"
        }
      + tags_all                        = {
          + "Name" = "my-3-tier-architecture-vpc-db-us-west-2c"
        }
      + vpc_id                          = (known after apply)
    }

  # module.networking.module.vpc.aws_subnet.private[0] will be created
  + resource "aws_subnet" "private" {
      + arn                             = (known after apply)
      + assign_ipv6_address_on_creation = false
      + availability_zone               = "us-west-2a"
      + availability_zone_id            = (known after apply)
      + cidr_block                      = "10.0.1.0/24"
      + id                              = (known after apply)
      + ipv6_cidr_block_association_id  = (known after apply)
      + map_public_ip_on_launch         = false
      + owner_id                        = (known after apply)
      + tags                            = {
          + "Name" = "my-3-tier-architecture-vpc-private-us-west-2a"
        }
      + tags_all                        = {
          + "Name" = "my-3-tier-architecture-vpc-private-us-west-2a"
        }
      + vpc_id                          = (known after apply)
    }

  # module.networking.module.vpc.aws_subnet.private[1] will be created
  + resource "aws_subnet" "private" {
      + arn                             = (known after apply)
      + assign_ipv6_address_on_creation = false
      + availability_zone               = "us-west-2b"
      + availability_zone_id            = (known after apply)
      + cidr_block                      = "10.0.2.0/24"
      + id                              = (known after apply)
      + ipv6_cidr_block_association_id  = (known after apply)
      + map_public_ip_on_launch         = false
      + owner_id                        = (known after apply)
      + tags                            = {
          + "Name" = "my-3-tier-architecture-vpc-private-us-west-2b"
        }
      + tags_all                        = {
          + "Name" = "my-3-tier-architecture-vpc-private-us-west-2b"
        }
      + vpc_id                          = (known after apply)
    }

  # module.networking.module.vpc.aws_subnet.private[2] will be created
  + resource "aws_subnet" "private" {
      + arn                             = (known after apply)
      + assign_ipv6_address_on_creation = false
      + availability_zone               = "us-west-2c"
      + availability_zone_id            = (known after apply)
      + cidr_block                      = "10.0.3.0/24"
      + id                              = (known after apply)
      + ipv6_cidr_block_association_id  = (known after apply)
      + map_public_ip_on_launch         = false
      + owner_id                        = (known after apply)
      + tags                            = {
          + "Name" = "my-3-tier-architecture-vpc-private-us-west-2c"
        }
      + tags_all                        = {
          + "Name" = "my-3-tier-architecture-vpc-private-us-west-2c"
        }
      + vpc_id                          = (known after apply)
    }

  # module.networking.module.vpc.aws_subnet.public[0] will be created
  + resource "aws_subnet" "public" {
      + arn                             = (known after apply)
      + assign_ipv6_address_on_creation = false
      + availability_zone               = "us-west-2a"
      + availability_zone_id            = (known after apply)
      + cidr_block                      = "10.0.101.0/24"
      + id                              = (known after apply)
      + ipv6_cidr_block_association_id  = (known after apply)
      + map_public_ip_on_launch         = true
      + owner_id                        = (known after apply)
      + tags                            = {
          + "Name" = "my-3-tier-architecture-vpc-public-us-west-2a"
        }
      + tags_all                        = {
          + "Name" = "my-3-tier-architecture-vpc-public-us-west-2a"
        }
      + vpc_id                          = (known after apply)
    }

  # module.networking.module.vpc.aws_subnet.public[1] will be created
  + resource "aws_subnet" "public" {
      + arn                             = (known after apply)
      + assign_ipv6_address_on_creation = false
      + availability_zone               = "us-west-2b"
      + availability_zone_id            = (known after apply)
      + cidr_block                      = "10.0.102.0/24"
      + id                              = (known after apply)
      + ipv6_cidr_block_association_id  = (known after apply)
      + map_public_ip_on_launch         = true
      + owner_id                        = (known after apply)
      + tags                            = {
          + "Name" = "my-3-tier-architecture-vpc-public-us-west-2b"
        }
      + tags_all                        = {
          + "Name" = "my-3-tier-architecture-vpc-public-us-west-2b"
        }
      + vpc_id                          = (known after apply)
    }

  # module.networking.module.vpc.aws_subnet.public[2] will be created
  + resource "aws_subnet" "public" {
      + arn                             = (known after apply)
      + assign_ipv6_address_on_creation = false
      + availability_zone               = "us-west-2c"
      + availability_zone_id            = (known after apply)
      + cidr_block                      = "10.0.103.0/24"
      + id                              = (known after apply)
      + ipv6_cidr_block_association_id  = (known after apply)
      + map_public_ip_on_launch         = true
      + owner_id                        = (known after apply)
      + tags                            = {
          + "Name" = "my-3-tier-architecture-vpc-public-us-west-2c"
        }
      + tags_all                        = {
          + "Name" = "my-3-tier-architecture-vpc-public-us-west-2c"
        }
      + vpc_id                          = (known after apply)
    }

  # module.networking.module.vpc.aws_vpc.this[0] will be created
  + resource "aws_vpc" "this" {
      + arn                              = (known after apply)
      + assign_generated_ipv6_cidr_block = false
      + cidr_block                       = "10.0.0.0/16"
      + default_network_acl_id           = (known after apply)
      + default_route_table_id           = (known after apply)
      + default_security_group_id        = (known after apply)
      + dhcp_options_id                  = (known after apply)
      + enable_classiclink               = (known after apply)
      + enable_classiclink_dns_support   = (known after apply)
      + enable_dns_hostnames             = false
      + enable_dns_support               = true
      + id                               = (known after apply)
      + instance_tenancy                 = "default"
      + ipv6_association_id              = (known after apply)
      + ipv6_cidr_block                  = (known after apply)
      + main_route_table_id              = (known after apply)
      + owner_id                         = (known after apply)
      + tags                             = {
          + "Name" = "my-3-tier-architecture-vpc"
        }
      + tags_all                         = {
          + "Name" = "my-3-tier-architecture-vpc"
        }
    }

  # module.networking.module.websvr_sg.aws_security_group.security_group will be created
  + resource "aws_security_group" "security_group" {
      + arn                    = (known after apply)
      + description            = "Managed by Terraform"
      + egress                 = [
          + {
              + cidr_blocks      = [
                  + "0.0.0.0/0",
                ]
              + description      = ""
              + from_port        = 0
              + ipv6_cidr_blocks = []
              + prefix_list_ids  = []
              + protocol         = "-1"
              + security_groups  = []
              + self             = false
              + to_port          = 0
            },
        ]
      + id                     = (known after apply)
      + ingress                = [
          + {
              + cidr_blocks      = [
                  + "10.0.0.0/16",
                ]
              + description      = ""
              + from_port        = 22
              + ipv6_cidr_blocks = []
              + prefix_list_ids  = []
              + protocol         = "tcp"
              + security_groups  = []
              + self             = false
              + to_port          = 22
            },
          + {
              + cidr_blocks      = []
              + description      = ""
              + from_port        = 0
              + ipv6_cidr_blocks = []
              + prefix_list_ids  = []
              + protocol         = "-1"
              + security_groups  = []
              + self             = true
              + to_port          = 0
            },
          + {
              + cidr_blocks      = []
              + description      = ""
              + from_port        = 8080
              + ipv6_cidr_blocks = []
              + prefix_list_ids  = []
              + protocol         = "tcp"
              + security_groups  = (known after apply)
              + self             = false
              + to_port          = 8080
            },
        ]
      + name                   = (known after apply)
      + name_prefix            = (known after apply)
      + owner_id               = (known after apply)
      + revoke_rules_on_delete = false
      + tags_all               = (known after apply)
      + vpc_id                 = (known after apply)
    }

Plan: 40 to add, 0 to change, 0 to destroy.

Changes to Outputs:
  + db_password = (sensitive value)
  + lb_dns_name = (known after apply)

─────────────────────────────────────────────────────────────────────────────

Note: You didn't use the -out option to save this plan, so Terraform can't
guarantee to take exactly these actions if you run "terraform apply" now.

Admin@DevOps MINGW64 ~/Desktop/test/3-tier-architecture (main)
$


Admin@DevOps MINGW64 ~/Desktop/test/3-tier-architecture (main)
$


Admin@DevOps MINGW64 ~/Desktop/test/3-tier-architecture (main)
$


Admin@DevOps MINGW64 ~/Desktop/test/3-tier-architecture (main)
$

Admin@DevOps MINGW64 ~/Desktop/test/3-tier-architecture (main)
$ terraform apply

Terraform used the selected providers to generate the following execution
plan. Resource actions are indicated with the following symbols:
  + create
 <= read (data resources)

Terraform will perform the following actions:

  # module.autoscaling.data.cloudinit_config.config will be read during apply
  # (config refers to values not yet known)
 <= data "cloudinit_config" "config"  {
      + base64_encode = true
      + gzip          = true
      + id            = (known after apply)
      + rendered      = (known after apply)

      + part {
          + content      = (sensitive)
          + content_type = "text/cloud-config"
        }
    }

  # module.autoscaling.aws_autoscaling_group.webserver will be created
  + resource "aws_autoscaling_group" "webserver" {
      + arn                       = (known after apply)
      + availability_zones        = (known after apply)
      + default_cooldown          = (known after apply)
      + desired_capacity          = (known after apply)
      + force_delete              = false
      + force_delete_warm_pool    = false
      + health_check_grace_period = 300
      + health_check_type         = (known after apply)
      + id                        = (known after apply)
      + max_size                  = 3
      + metrics_granularity       = "1Minute"
      + min_size                  = 1
      + name                      = "my-3-tier-architecture-asg"
      + name_prefix               = (known after apply)
      + protect_from_scale_in     = false
      + service_linked_role_arn   = (known after apply)
      + target_group_arns         = (known after apply)
      + vpc_zone_identifier       = (known after apply)
      + wait_for_capacity_timeout = "10m"

      + launch_template {
          + id      = (known after apply)
          + name    = (known after apply)
          + version = (known after apply)
        }
    }

  # module.autoscaling.aws_launch_template.webserver will be created
  + resource "aws_launch_template" "webserver" {
      + arn                    = (known after apply)
      + default_version        = (known after apply)
      + id                     = (known after apply)
      + image_id               = "ami-074251216af698218"
      + instance_type          = "t2.micro"
      + latest_version         = (known after apply)
      + name                   = (known after apply)
      + name_prefix            = "my-3-tier-architecture"
      + tags_all               = (known after apply)
      + user_data              = (known after apply)
      + vpc_security_group_ids = (known after apply)

      + iam_instance_profile {
          + name = (known after apply)
        }

      + metadata_options {
          + http_endpoint               = (known after apply)
          + http_protocol_ipv6          = (known after apply)
          + http_put_response_hop_limit = (known after apply)
          + http_tokens                 = (known after apply)
        }
    }

  # module.database.aws_db_instance.database will be created
  + resource "aws_db_instance" "database" {
      + address                               = (known after apply)
      + allocated_storage                     = 10
      + apply_immediately                     = (known after apply)
      + arn                                   = (known after apply)
      + auto_minor_version_upgrade            = true
      + availability_zone                     = (known after apply)
      + backup_retention_period               = (known after apply)
      + backup_window                         = (known after apply)
      + ca_cert_identifier                    = (known after apply)
      + character_set_name                    = (known after apply)
      + copy_tags_to_snapshot                 = false
      + db_subnet_group_name                  = (known after apply)
      + delete_automated_backups              = true
      + endpoint                              = (known after apply)
      + engine                                = "mysql"
      + engine_version                        = "8.0"
      + engine_version_actual                 = (known after apply)
      + hosted_zone_id                        = (known after apply)
      + id                                    = (known after apply)
      + identifier                            = "my-3-tier-architecture-db-instance"
      + identifier_prefix                     = (known after apply)
      + instance_class                        = "db.t2.micro"
      + kms_key_id                            = (known after apply)
      + latest_restorable_time                = (known after apply)
      + license_model                         = (known after apply)
      + maintenance_window                    = (known after apply)
      + monitoring_interval                   = 0
      + monitoring_role_arn                   = (known after apply)
      + multi_az                              = (known after apply)
      + name                                  = "pets"
      + nchar_character_set_name              = (known after apply)
      + option_group_name                     = (known after apply)
      + parameter_group_name                  = (known after apply)
      + password                              = (sensitive value)
      + performance_insights_enabled          = false
      + performance_insights_kms_key_id       = (known after apply)
      + performance_insights_retention_period = (known after apply)
      + port                                  = (known after apply)
      + publicly_accessible                   = false
      + replicas                              = (known after apply)
      + resource_id                           = (known after apply)
      + skip_final_snapshot                   = true
      + snapshot_identifier                   = (known after apply)
      + status                                = (known after apply)
      + storage_type                          = (known after apply)
      + tags_all                              = (known after apply)
      + timezone                              = (known after apply)
      + username                              = "admin"
      + vpc_security_group_ids                = (known after apply)
    }

  # module.database.random_password.password will be created
  + resource "random_password" "password" {
      + id               = (known after apply)
      + length           = 16
      + lower            = true
      + min_lower        = 0
      + min_numeric      = 0
      + min_special      = 0
      + min_upper        = 0
      + number           = true
      + override_special = "_%@/'\""
      + result           = (sensitive value)
      + special          = true
      + upper            = true
    }

  # module.autoscaling.module.alb.aws_lb.this[0] will be created
  + resource "aws_lb" "this" {
      + arn                        = (known after apply)
      + arn_suffix                 = (known after apply)
      + dns_name                   = (known after apply)
      + drop_invalid_header_fields = false
      + enable_deletion_protection = false
      + enable_http2               = true
      + id                         = (known after apply)
      + idle_timeout               = 60
      + internal                   = false
      + ip_address_type            = "ipv4"
      + load_balancer_type         = "application"
      + name                       = "my-3-tier-architecture"
      + security_groups            = (known after apply)
      + subnets                    = (known after apply)
      + tags                       = {
          + "Name" = "my-3-tier-architecture"
        }
      + tags_all                   = {
          + "Name" = "my-3-tier-architecture"
        }
      + vpc_id                     = (known after apply)
      + zone_id                    = (known after apply)

      + subnet_mapping {
          + allocation_id        = (known after apply)
          + ipv6_address         = (known after apply)
          + outpost_id           = (known after apply)
          + private_ipv4_address = (known after apply)
          + subnet_id            = (known after apply)
        }

      + timeouts {
          + create = "10m"
          + delete = "10m"
          + update = "10m"
        }
    }

  # module.autoscaling.module.alb.aws_lb_listener.frontend_http_tcp[0] will be created
  + resource "aws_lb_listener" "frontend_http_tcp" {
      + arn               = (known after apply)
      + id                = (known after apply)
      + load_balancer_arn = (known after apply)
      + port              = 80
      + protocol          = "HTTP"
      + ssl_policy        = (known after apply)
      + tags_all          = (known after apply)

      + default_action {
          + order            = (known after apply)
          + target_group_arn = (known after apply)
          + type             = "forward"
        }
    }

  # module.autoscaling.module.alb.aws_lb_target_group.main[0] will be created
  + resource "aws_lb_target_group" "main" {
      + arn                                = (known after apply)
      + arn_suffix                         = (known after apply)
      + deregistration_delay               = "300"
      + id                                 = (known after apply)
      + lambda_multi_value_headers_enabled = false
      + load_balancing_algorithm_type      = (known after apply)
      + name                               = (known after apply)
      + name_prefix                        = "websvr"
      + port                               = 8080
      + preserve_client_ip                 = (known after apply)
      + protocol                           = "HTTP"
      + protocol_version                   = (known after apply)
      + proxy_protocol_v2                  = false
      + slow_start                         = 0
      + tags                               = {
          + "Name" = "websvr"
        }
      + tags_all                           = {
          + "Name" = "websvr"
        }
      + target_type                        = "instance"
      + vpc_id                             = (known after apply)

      + health_check {
          + enabled             = (known after apply)
          + healthy_threshold   = (known after apply)
          + interval            = (known after apply)
          + matcher             = (known after apply)
          + path                = (known after apply)
          + port                = (known after apply)
          + protocol            = (known after apply)
          + timeout             = (known after apply)
          + unhealthy_threshold = (known after apply)
        }

      + stickiness {
          + cookie_duration = (known after apply)
          + cookie_name     = (known after apply)
          + enabled         = (known after apply)
          + type            = (known after apply)
        }
    }

  # module.autoscaling.module.iam_instance_profile.aws_iam_instance_profile.iam_instance_profile will be created
  + resource "aws_iam_instance_profile" "iam_instance_profile" {
      + arn         = (known after apply)
      + create_date = (known after apply)
      + id          = (known after apply)
      + name        = (known after apply)
      + path        = "/"
      + role        = (known after apply)
      + tags_all    = (known after apply)
      + unique_id   = (known after apply)
    }

  # module.autoscaling.module.iam_instance_profile.aws_iam_role.iam_role will be created
  + resource "aws_iam_role" "iam_role" {
      + arn                   = (known after apply)
      + assume_role_policy    = jsonencode(
            {
              + Statement = [
                  + {
                      + Action    = "sts:AssumeRole"
                      + Effect    = "Allow"
                      + Principal = {
                          + Service = "ec2.amazonaws.com"
                        }
                    },
                ]
              + Version   = "2012-10-17"
            }
        )
      + create_date           = (known after apply)
      + force_detach_policies = false
      + id                    = (known after apply)
      + managed_policy_arns   = (known after apply)
      + max_session_duration  = 3600
      + name                  = (known after apply)
      + name_prefix           = (known after apply)
      + path                  = "/"
      + tags_all              = (known after apply)
      + unique_id             = (known after apply)

      + inline_policy {
          + name   = (known after apply)
          + policy = (known after apply)
        }
    }

  # module.autoscaling.module.iam_instance_profile.aws_iam_role_policy.iam_role_policy will be created
  + resource "aws_iam_role_policy" "iam_role_policy" {
      + id     = (known after apply)
      + name   = (known after apply)
      + policy = jsonencode(
            {
              + Statement = [
                  + {
                      + Action   = [
                          + "rds:*",
                          + "logs:*",
                        ]
                      + Effect   = "Allow"
                      + Resource = "*"
                      + Sid      = ""
                    },
                ]
              + Version   = "2012-10-17"
            }
        )
      + role   = (known after apply)
    }

  # module.networking.module.db_sg.aws_security_group.security_group will be created
  + resource "aws_security_group" "security_group" {
      + arn                    = (known after apply)
      + description            = "Managed by Terraform"
      + egress                 = [
          + {
              + cidr_blocks      = [
                  + "0.0.0.0/0",
                ]
              + description      = ""
              + from_port        = 0
              + ipv6_cidr_blocks = []
              + prefix_list_ids  = []
              + protocol         = "-1"
              + security_groups  = []
              + self             = false
              + to_port          = 0
            },
        ]
      + id                     = (known after apply)
      + ingress                = [
          + {
              + cidr_blocks      = []
              + description      = ""
              + from_port        = 0
              + ipv6_cidr_blocks = []
              + prefix_list_ids  = []
              + protocol         = "-1"
              + security_groups  = []
              + self             = true
              + to_port          = 0
            },
          + {
              + cidr_blocks      = []
              + description      = ""
              + from_port        = 3306
              + ipv6_cidr_blocks = []
              + prefix_list_ids  = []
              + protocol         = "tcp"
              + security_groups  = (known after apply)
              + self             = false
              + to_port          = 3306
            },
        ]
      + name                   = (known after apply)
      + name_prefix            = (known after apply)
      + owner_id               = (known after apply)
      + revoke_rules_on_delete = false
      + tags_all               = (known after apply)
      + vpc_id                 = (known after apply)
    }

  # module.networking.module.lb_sg.aws_security_group.security_group will be created
  + resource "aws_security_group" "security_group" {
      + arn                    = (known after apply)
      + description            = "Managed by Terraform"
      + egress                 = [
          + {
              + cidr_blocks      = [
                  + "0.0.0.0/0",
                ]
              + description      = ""
              + from_port        = 0
              + ipv6_cidr_blocks = []
              + prefix_list_ids  = []
              + protocol         = "-1"
              + security_groups  = []
              + self             = false
              + to_port          = 0
            },
        ]
      + id                     = (known after apply)
      + ingress                = [
          + {
              + cidr_blocks      = [
                  + "0.0.0.0/0",
                ]
              + description      = ""
              + from_port        = 80
              + ipv6_cidr_blocks = []
              + prefix_list_ids  = []
              + protocol         = "tcp"
              + security_groups  = []
              + self             = false
              + to_port          = 80
            },
          + {
              + cidr_blocks      = []
              + description      = ""
              + from_port        = 0
              + ipv6_cidr_blocks = []
              + prefix_list_ids  = []
              + protocol         = "-1"
              + security_groups  = []
              + self             = true
              + to_port          = 0
            },
        ]
      + name                   = (known after apply)
      + name_prefix            = (known after apply)
      + owner_id               = (known after apply)
      + revoke_rules_on_delete = false
      + tags_all               = (known after apply)
      + vpc_id                 = (known after apply)
    }

  # module.networking.module.vpc.aws_db_subnet_group.database[0] will be created
  + resource "aws_db_subnet_group" "database" {
      + arn         = (known after apply)
      + description = "Database subnet group for my-3-tier-architecture-vpc"
      + id          = (known after apply)
      + name        = "my-3-tier-architecture-vpc"
      + name_prefix = (known after apply)
      + subnet_ids  = (known after apply)
      + tags        = {
          + "Name" = "my-3-tier-architecture-vpc"
        }
      + tags_all    = {
          + "Name" = "my-3-tier-architecture-vpc"
        }
    }

  # module.networking.module.vpc.aws_eip.nat[0] will be created
  + resource "aws_eip" "nat" {
      + allocation_id        = (known after apply)
      + association_id       = (known after apply)
      + carrier_ip           = (known after apply)
      + customer_owned_ip    = (known after apply)
      + domain               = (known after apply)
      + id                   = (known after apply)
      + instance             = (known after apply)
      + network_border_group = (known after apply)
      + network_interface    = (known after apply)
      + private_dns          = (known after apply)
      + private_ip           = (known after apply)
      + public_dns           = (known after apply)
      + public_ip            = (known after apply)
      + public_ipv4_pool     = (known after apply)
      + tags                 = {
          + "Name" = "my-3-tier-architecture-vpc-us-west-2a"
        }
      + tags_all             = {
          + "Name" = "my-3-tier-architecture-vpc-us-west-2a"
        }
      + vpc                  = true
    }

  # module.networking.module.vpc.aws_internet_gateway.this[0] will be created
  + resource "aws_internet_gateway" "this" {
      + arn      = (known after apply)
      + id       = (known after apply)
      + owner_id = (known after apply)
      + tags     = {
          + "Name" = "my-3-tier-architecture-vpc"
        }
      + tags_all = {
          + "Name" = "my-3-tier-architecture-vpc"
        }
      + vpc_id   = (known after apply)
    }

  # module.networking.module.vpc.aws_nat_gateway.this[0] will be created
  + resource "aws_nat_gateway" "this" {
      + allocation_id        = (known after apply)
      + connectivity_type    = "public"
      + id                   = (known after apply)
      + network_interface_id = (known after apply)
      + private_ip           = (known after apply)
      + public_ip            = (known after apply)
      + subnet_id            = (known after apply)
      + tags                 = {
          + "Name" = "my-3-tier-architecture-vpc-us-west-2a"
        }
      + tags_all             = {
          + "Name" = "my-3-tier-architecture-vpc-us-west-2a"
        }
    }

  # module.networking.module.vpc.aws_route.private_nat_gateway[0] will be created
  + resource "aws_route" "private_nat_gateway" {
      + destination_cidr_block = "0.0.0.0/0"
      + id                     = (known after apply)
      + instance_id            = (known after apply)
      + instance_owner_id      = (known after apply)
      + nat_gateway_id         = (known after apply)
      + network_interface_id   = (known after apply)
      + origin                 = (known after apply)
      + route_table_id         = (known after apply)
      + state                  = (known after apply)

      + timeouts {
          + create = "5m"
        }
    }

  # module.networking.module.vpc.aws_route.public_internet_gateway[0] will be created
  + resource "aws_route" "public_internet_gateway" {
      + destination_cidr_block = "0.0.0.0/0"
      + gateway_id             = (known after apply)
      + id                     = (known after apply)
      + instance_id            = (known after apply)
      + instance_owner_id      = (known after apply)
      + network_interface_id   = (known after apply)
      + origin                 = (known after apply)
      + route_table_id         = (known after apply)
      + state                  = (known after apply)

      + timeouts {
          + create = "5m"
        }
    }

  # module.networking.module.vpc.aws_route_table.private[0] will be created
  + resource "aws_route_table" "private" {
      + arn              = (known after apply)
      + id               = (known after apply)
      + owner_id         = (known after apply)
      + propagating_vgws = (known after apply)
      + route            = (known after apply)
      + tags             = {
          + "Name" = "my-3-tier-architecture-vpc-private"
        }
      + tags_all         = {
          + "Name" = "my-3-tier-architecture-vpc-private"
        }
      + vpc_id           = (known after apply)
    }

  # module.networking.module.vpc.aws_route_table.public[0] will be created
  + resource "aws_route_table" "public" {
      + arn              = (known after apply)
      + id               = (known after apply)
      + owner_id         = (known after apply)
      + propagating_vgws = (known after apply)
      + route            = (known after apply)
      + tags             = {
          + "Name" = "my-3-tier-architecture-vpc-public"
        }
      + tags_all         = {
          + "Name" = "my-3-tier-architecture-vpc-public"
        }
      + vpc_id           = (known after apply)
    }

  # module.networking.module.vpc.aws_route_table_association.database[0] will be created
  + resource "aws_route_table_association" "database" {
      + id             = (known after apply)
      + route_table_id = (known after apply)
      + subnet_id      = (known after apply)
    }

  # module.networking.module.vpc.aws_route_table_association.database[1] will be created
  + resource "aws_route_table_association" "database" {
      + id             = (known after apply)
      + route_table_id = (known after apply)
      + subnet_id      = (known after apply)
    }

  # module.networking.module.vpc.aws_route_table_association.database[2] will be created
  + resource "aws_route_table_association" "database" {
      + id             = (known after apply)
      + route_table_id = (known after apply)
      + subnet_id      = (known after apply)
    }

  # module.networking.module.vpc.aws_route_table_association.private[0] will be created
  + resource "aws_route_table_association" "private" {
      + id             = (known after apply)
      + route_table_id = (known after apply)
      + subnet_id      = (known after apply)
    }

  # module.networking.module.vpc.aws_route_table_association.private[1] will be created
  + resource "aws_route_table_association" "private" {
      + id             = (known after apply)
      + route_table_id = (known after apply)
      + subnet_id      = (known after apply)
    }

  # module.networking.module.vpc.aws_route_table_association.private[2] will be created
  + resource "aws_route_table_association" "private" {
      + id             = (known after apply)
      + route_table_id = (known after apply)
      + subnet_id      = (known after apply)
    }

  # module.networking.module.vpc.aws_route_table_association.public[0] will be created
  + resource "aws_route_table_association" "public" {
      + id             = (known after apply)
      + route_table_id = (known after apply)
      + subnet_id      = (known after apply)
    }

  # module.networking.module.vpc.aws_route_table_association.public[1] will be created
  + resource "aws_route_table_association" "public" {
      + id             = (known after apply)
      + route_table_id = (known after apply)
      + subnet_id      = (known after apply)
    }

  # module.networking.module.vpc.aws_route_table_association.public[2] will be created
  + resource "aws_route_table_association" "public" {
      + id             = (known after apply)
      + route_table_id = (known after apply)
      + subnet_id      = (known after apply)
    }

  # module.networking.module.vpc.aws_subnet.database[0] will be created
  + resource "aws_subnet" "database" {
      + arn                             = (known after apply)
      + assign_ipv6_address_on_creation = false
      + availability_zone               = "us-west-2a"
      + availability_zone_id            = (known after apply)
      + cidr_block                      = "10.0.21.0/24"
      + id                              = (known after apply)
      + ipv6_cidr_block_association_id  = (known after apply)
      + map_public_ip_on_launch         = false
      + owner_id                        = (known after apply)
      + tags                            = {
          + "Name" = "my-3-tier-architecture-vpc-db-us-west-2a"
        }
      + tags_all                        = {
          + "Name" = "my-3-tier-architecture-vpc-db-us-west-2a"
        }
      + vpc_id                          = (known after apply)
    }

  # module.networking.module.vpc.aws_subnet.database[1] will be created
  + resource "aws_subnet" "database" {
      + arn                             = (known after apply)
      + assign_ipv6_address_on_creation = false
      + availability_zone               = "us-west-2b"
      + availability_zone_id            = (known after apply)
      + cidr_block                      = "10.0.22.0/24"
      + id                              = (known after apply)
      + ipv6_cidr_block_association_id  = (known after apply)
      + map_public_ip_on_launch         = false
      + owner_id                        = (known after apply)
      + tags                            = {
          + "Name" = "my-3-tier-architecture-vpc-db-us-west-2b"
        }
      + tags_all                        = {
          + "Name" = "my-3-tier-architecture-vpc-db-us-west-2b"
        }
      + vpc_id                          = (known after apply)
    }

  # module.networking.module.vpc.aws_subnet.database[2] will be created
  + resource "aws_subnet" "database" {
      + arn                             = (known after apply)
      + assign_ipv6_address_on_creation = false
      + availability_zone               = "us-west-2c"
      + availability_zone_id            = (known after apply)
      + cidr_block                      = "10.0.23.0/24"
      + id                              = (known after apply)
      + ipv6_cidr_block_association_id  = (known after apply)
      + map_public_ip_on_launch         = false
      + owner_id                        = (known after apply)
      + tags                            = {
          + "Name" = "my-3-tier-architecture-vpc-db-us-west-2c"
        }
      + tags_all                        = {
          + "Name" = "my-3-tier-architecture-vpc-db-us-west-2c"
        }
      + vpc_id                          = (known after apply)
    }

  # module.networking.module.vpc.aws_subnet.private[0] will be created
  + resource "aws_subnet" "private" {
      + arn                             = (known after apply)
      + assign_ipv6_address_on_creation = false
      + availability_zone               = "us-west-2a"
      + availability_zone_id            = (known after apply)
      + cidr_block                      = "10.0.1.0/24"
      + id                              = (known after apply)
      + ipv6_cidr_block_association_id  = (known after apply)
      + map_public_ip_on_launch         = false
      + owner_id                        = (known after apply)
      + tags                            = {
          + "Name" = "my-3-tier-architecture-vpc-private-us-west-2a"
        }
      + tags_all                        = {
          + "Name" = "my-3-tier-architecture-vpc-private-us-west-2a"
        }
      + vpc_id                          = (known after apply)
    }

  # module.networking.module.vpc.aws_subnet.private[1] will be created
  + resource "aws_subnet" "private" {
      + arn                             = (known after apply)
      + assign_ipv6_address_on_creation = false
      + availability_zone               = "us-west-2b"
      + availability_zone_id            = (known after apply)
      + cidr_block                      = "10.0.2.0/24"
      + id                              = (known after apply)
      + ipv6_cidr_block_association_id  = (known after apply)
      + map_public_ip_on_launch         = false
      + owner_id                        = (known after apply)
      + tags                            = {
          + "Name" = "my-3-tier-architecture-vpc-private-us-west-2b"
        }
      + tags_all                        = {
          + "Name" = "my-3-tier-architecture-vpc-private-us-west-2b"
        }
      + vpc_id                          = (known after apply)
    }

  # module.networking.module.vpc.aws_subnet.private[2] will be created
  + resource "aws_subnet" "private" {
      + arn                             = (known after apply)
      + assign_ipv6_address_on_creation = false
      + availability_zone               = "us-west-2c"
      + availability_zone_id            = (known after apply)
      + cidr_block                      = "10.0.3.0/24"
      + id                              = (known after apply)
      + ipv6_cidr_block_association_id  = (known after apply)
      + map_public_ip_on_launch         = false
      + owner_id                        = (known after apply)
      + tags                            = {
          + "Name" = "my-3-tier-architecture-vpc-private-us-west-2c"
        }
      + tags_all                        = {
          + "Name" = "my-3-tier-architecture-vpc-private-us-west-2c"
        }
      + vpc_id                          = (known after apply)
    }

  # module.networking.module.vpc.aws_subnet.public[0] will be created
  + resource "aws_subnet" "public" {
      + arn                             = (known after apply)
      + assign_ipv6_address_on_creation = false
      + availability_zone               = "us-west-2a"
      + availability_zone_id            = (known after apply)
      + cidr_block                      = "10.0.101.0/24"
      + id                              = (known after apply)
      + ipv6_cidr_block_association_id  = (known after apply)
      + map_public_ip_on_launch         = true
      + owner_id                        = (known after apply)
      + tags                            = {
          + "Name" = "my-3-tier-architecture-vpc-public-us-west-2a"
        }
      + tags_all                        = {
          + "Name" = "my-3-tier-architecture-vpc-public-us-west-2a"
        }
      + vpc_id                          = (known after apply)
    }

  # module.networking.module.vpc.aws_subnet.public[1] will be created
  + resource "aws_subnet" "public" {
      + arn                             = (known after apply)
      + assign_ipv6_address_on_creation = false
      + availability_zone               = "us-west-2b"
      + availability_zone_id            = (known after apply)
      + cidr_block                      = "10.0.102.0/24"
      + id                              = (known after apply)
      + ipv6_cidr_block_association_id  = (known after apply)
      + map_public_ip_on_launch         = true
      + owner_id                        = (known after apply)
      + tags                            = {
          + "Name" = "my-3-tier-architecture-vpc-public-us-west-2b"
        }
      + tags_all                        = {
          + "Name" = "my-3-tier-architecture-vpc-public-us-west-2b"
        }
      + vpc_id                          = (known after apply)
    }

  # module.networking.module.vpc.aws_subnet.public[2] will be created
  + resource "aws_subnet" "public" {
      + arn                             = (known after apply)
      + assign_ipv6_address_on_creation = false
      + availability_zone               = "us-west-2c"
      + availability_zone_id            = (known after apply)
      + cidr_block                      = "10.0.103.0/24"
      + id                              = (known after apply)
      + ipv6_cidr_block_association_id  = (known after apply)
      + map_public_ip_on_launch         = true
      + owner_id                        = (known after apply)
      + tags                            = {
          + "Name" = "my-3-tier-architecture-vpc-public-us-west-2c"
        }
      + tags_all                        = {
          + "Name" = "my-3-tier-architecture-vpc-public-us-west-2c"
        }
      + vpc_id                          = (known after apply)
    }

  # module.networking.module.vpc.aws_vpc.this[0] will be created
  + resource "aws_vpc" "this" {
      + arn                              = (known after apply)
      + assign_generated_ipv6_cidr_block = false
      + cidr_block                       = "10.0.0.0/16"
      + default_network_acl_id           = (known after apply)
      + default_route_table_id           = (known after apply)
      + default_security_group_id        = (known after apply)
      + dhcp_options_id                  = (known after apply)
      + enable_classiclink               = (known after apply)
      + enable_classiclink_dns_support   = (known after apply)
      + enable_dns_hostnames             = false
      + enable_dns_support               = true
      + id                               = (known after apply)
      + instance_tenancy                 = "default"
      + ipv6_association_id              = (known after apply)
      + ipv6_cidr_block                  = (known after apply)
      + main_route_table_id              = (known after apply)
      + owner_id                         = (known after apply)
      + tags                             = {
          + "Name" = "my-3-tier-architecture-vpc"
        }
      + tags_all                         = {
          + "Name" = "my-3-tier-architecture-vpc"
        }
    }

  # module.networking.module.websvr_sg.aws_security_group.security_group will be created
  + resource "aws_security_group" "security_group" {
      + arn                    = (known after apply)
      + description            = "Managed by Terraform"
      + egress                 = [
          + {
              + cidr_blocks      = [
                  + "0.0.0.0/0",
                ]
              + description      = ""
              + from_port        = 0
              + ipv6_cidr_blocks = []
              + prefix_list_ids  = []
              + protocol         = "-1"
              + security_groups  = []
              + self             = false
              + to_port          = 0
            },
        ]
      + id                     = (known after apply)
      + ingress                = [
          + {
              + cidr_blocks      = [
                  + "10.0.0.0/16",
                ]
              + description      = ""
              + from_port        = 22
              + ipv6_cidr_blocks = []
              + prefix_list_ids  = []
              + protocol         = "tcp"
              + security_groups  = []
              + self             = false
              + to_port          = 22
            },
          + {
              + cidr_blocks      = []
              + description      = ""
              + from_port        = 0
              + ipv6_cidr_blocks = []
              + prefix_list_ids  = []
              + protocol         = "-1"
              + security_groups  = []
              + self             = true
              + to_port          = 0
            },
          + {
              + cidr_blocks      = []
              + description      = ""
              + from_port        = 8080
              + ipv6_cidr_blocks = []
              + prefix_list_ids  = []
              + protocol         = "tcp"
              + security_groups  = (known after apply)
              + self             = false
              + to_port          = 8080
            },
        ]
      + name                   = (known after apply)
      + name_prefix            = (known after apply)
      + owner_id               = (known after apply)
      + revoke_rules_on_delete = false
      + tags_all               = (known after apply)
      + vpc_id                 = (known after apply)
    }

Plan: 40 to add, 0 to change, 0 to destroy.

Changes to Outputs:
  + db_password = (sensitive value)
  + lb_dns_name = (known after apply)

Do you want to perform these actions?
  Terraform will perform the actions described above.
  Only 'yes' will be accepted to approve.

  Enter a value: yes

module.database.random_password.password: Creating...
module.database.random_password.password: Creation complete after 0s [id=none]
module.autoscaling.module.iam_instance_profile.aws_iam_role.iam_role: Creating...
module.networking.module.vpc.aws_vpc.this[0]: Creating...
module.networking.module.vpc.aws_eip.nat[0]: Creating...
module.networking.module.vpc.aws_eip.nat[0]: Creation complete after 2s [id=eipalloc-0c271d80e0b96839c]
module.autoscaling.module.iam_instance_profile.aws_iam_role.iam_role: Creation complete after 4s [id=terraform-20211209112432953600000001]
module.autoscaling.module.iam_instance_profile.aws_iam_role_policy.iam_role_policy: Creating...
module.autoscaling.module.iam_instance_profile.aws_iam_instance_profile.iam_instance_profile: Creating...
module.autoscaling.module.iam_instance_profile.aws_iam_role_policy.iam_role_policy: Creation complete after 1s [id=terraform-20211209112432953600000001:terraform-20211209112436676800000002]
module.autoscaling.module.iam_instance_profile.aws_iam_instance_profile.iam_instance_profile: Creation complete after 2s [id=terraform-20211209112436677900000003]
module.networking.module.vpc.aws_vpc.this[0]: Still creating... [10s elapsed]
module.networking.module.vpc.aws_vpc.this[0]: Creation complete after 12s [id=vpc-0e41b88411b107ccb]
module.networking.module.vpc.aws_internet_gateway.this[0]: Creating...
module.networking.module.vpc.aws_subnet.private[0]: Creating...
module.networking.module.vpc.aws_subnet.database[2]: Creating...
module.networking.module.vpc.aws_subnet.database[1]: Creating...
module.networking.module.vpc.aws_route_table.private[0]: Creating...
module.networking.module.vpc.aws_route_table.public[0]: Creating...
module.networking.module.vpc.aws_subnet.public[2]: Creating...
module.networking.module.vpc.aws_subnet.public[1]: Creating...
module.networking.module.vpc.aws_subnet.database[0]: Creating...
module.networking.module.vpc.aws_subnet.private[1]: Creating...
module.networking.module.vpc.aws_route_table.private[0]: Creation complete after 4s [id=rtb-0441f7cbd2720da87]
module.networking.module.vpc.aws_subnet.private[2]: Creating...
module.networking.module.vpc.aws_route_table.public[0]: Creation complete after 4s [id=rtb-0ef7909133d8f121e]
module.networking.module.vpc.aws_subnet.public[0]: Creating...
module.networking.module.vpc.aws_subnet.database[1]: Creation complete after 4s [id=subnet-0fa28647c54f6cb2b]
module.networking.module.vpc.aws_subnet.private[1]: Creation complete after 4s [id=subnet-098c5b2e22bec80c2]
module.networking.module.lb_sg.aws_security_group.security_group: Creating...
module.networking.module.vpc.aws_subnet.private[0]: Creation complete after 4s [id=subnet-0a21dbdfab358be99]
module.networking.module.vpc.aws_subnet.database[0]: Creation complete after 4s [id=subnet-04315cb26c7deb411]
module.networking.module.vpc.aws_subnet.database[2]: Creation complete after 4s [id=subnet-0925364cf17643020]
module.networking.module.vpc.aws_route_table_association.database[2]: Creating...
module.networking.module.vpc.aws_db_subnet_group.database[0]: Creating...
module.networking.module.vpc.aws_route_table_association.database[1]: Creating...
module.networking.module.vpc.aws_route_table_association.database[0]: Creating...
module.networking.module.vpc.aws_internet_gateway.this[0]: Creation complete after 6s [id=igw-0ef2ef5261f219c4a]
module.networking.module.vpc.aws_route.public_internet_gateway[0]: Creating...
module.networking.module.vpc.aws_subnet.private[2]: Creation complete after 4s [id=subnet-0e0ef959cd3f6ec9a]
module.networking.module.vpc.aws_route_table_association.private[2]: Creating...
module.networking.module.vpc.aws_route_table_association.database[2]: Creation complete after 4s [id=rtbassoc-09b002cdbe4859874]
module.networking.module.vpc.aws_route_table_association.private[1]: Creating...
module.networking.module.vpc.aws_route_table_association.database[0]: Creation complete after 4s [id=rtbassoc-056cda7f0ab4d0bd2]
module.networking.module.vpc.aws_route_table_association.private[0]: Creating...
module.networking.module.vpc.aws_route_table_association.database[1]: Creation complete after 4s [id=rtbassoc-07d45f374fe2558fa]
module.networking.module.vpc.aws_db_subnet_group.database[0]: Creation complete after 5s [id=my-3-tier-architecture-vpc]
module.networking.module.vpc.aws_subnet.public[2]: Still creating... [10s elapsed]
module.networking.module.vpc.aws_subnet.public[1]: Still creating... [10s elapsed]
module.networking.module.vpc.aws_route.public_internet_gateway[0]: Creation complete after 5s [id=r-rtb-0ef7909133d8f121e1080289494]
module.networking.module.vpc.aws_route_table_association.private[2]: Creation complete after 3s [id=rtbassoc-08e06733f874c2dc9]
module.networking.module.vpc.aws_route_table_association.private[1]: Creation complete after 3s [id=rtbassoc-09b6e92be25ec25a5]
module.networking.module.vpc.aws_route_table_association.private[0]: Creation complete after 3s [id=rtbassoc-093ad37d7dbcc9617]
module.networking.module.vpc.aws_subnet.public[0]: Still creating... [10s elapsed]
module.networking.module.lb_sg.aws_security_group.security_group: Creation complete after 10s [id=sg-0b7b411da05dccc53]
module.networking.module.websvr_sg.aws_security_group.security_group: Creating...
module.networking.module.vpc.aws_subnet.public[1]: Creation complete after 17s [id=subnet-0acce62e967c7df6c]
module.networking.module.vpc.aws_subnet.public[2]: Creation complete after 17s [id=subnet-06ea4d30c5e2bda51]
module.networking.module.vpc.aws_subnet.public[0]: Creation complete after 16s [id=subnet-0b5d9b86e26d2bd6a]
module.networking.module.vpc.aws_route_table_association.public[2]: Creating...
module.networking.module.vpc.aws_route_table_association.public[1]: Creating...
module.networking.module.vpc.aws_route_table_association.public[0]: Creating...
module.networking.module.vpc.aws_nat_gateway.this[0]: Creating...
module.networking.module.vpc.aws_route_table_association.public[0]: Creation complete after 3s [id=rtbassoc-0b8ffce252706c0bd]
module.networking.module.vpc.aws_route_table_association.public[2]: Creation complete after 3s [id=rtbassoc-006e03ba1bfe9ea3e]
module.networking.module.vpc.aws_route_table_association.public[1]: Creation complete after 3s [id=rtbassoc-0249675b9d2ada026]
module.networking.module.websvr_sg.aws_security_group.security_group: Creation complete after 10s [id=sg-0f7bb13cfc73fa728]
module.networking.module.db_sg.aws_security_group.security_group: Creating...
module.networking.module.vpc.aws_nat_gateway.this[0]: Still creating... [10s elapsed]
module.networking.module.db_sg.aws_security_group.security_group: Still creating... [10s elapsed]
module.networking.module.db_sg.aws_security_group.security_group: Creation complete after 10s [id=sg-0b119588cc0bd9170]
module.networking.module.vpc.aws_nat_gateway.this[0]: Still creating... [20s elapsed]
module.networking.module.vpc.aws_nat_gateway.this[0]: Still creating... [30s elapsed]
module.networking.module.vpc.aws_nat_gateway.this[0]: Still creating... [40s elapsed]
module.networking.module.vpc.aws_nat_gateway.this[0]: Still creating... [50s elapsed]
module.networking.module.vpc.aws_nat_gateway.this[0]: Still creating... [1m0s elapsed]
module.networking.module.vpc.aws_nat_gateway.this[0]: Still creating... [1m10s elapsed]
module.networking.module.vpc.aws_nat_gateway.this[0]: Still creating... [1m20s elapsed]
module.networking.module.vpc.aws_nat_gateway.this[0]: Still creating... [1m30s elapsed]
module.networking.module.vpc.aws_nat_gateway.this[0]: Still creating... [1m40s elapsed]
module.networking.module.vpc.aws_nat_gateway.this[0]: Still creating... [1m50s elapsed]
module.networking.module.vpc.aws_nat_gateway.this[0]: Creation complete after 1m52s [id=nat-03484b3d7f6c31716]
module.networking.module.vpc.aws_route.private_nat_gateway[0]: Creating...
module.networking.module.vpc.aws_route.private_nat_gateway[0]: Creation complete after 4s [id=r-rtb-0441f7cbd2720da871080289494]
module.autoscaling.module.alb.aws_lb.this[0]: Creating...
module.database.aws_db_instance.database: Creating...
module.autoscaling.module.alb.aws_lb.this[0]: Still creating... [10s elapsed]
module.database.aws_db_instance.database: Still creating... [10s elapsed]
module.autoscaling.module.alb.aws_lb.this[0]: Still creating... [20s elapsed]
module.database.aws_db_instance.database: Still creating... [20s elapsed]
module.autoscaling.module.alb.aws_lb.this[0]: Still creating... [30s elapsed]
module.database.aws_db_instance.database: Still creating... [30s elapsed]
module.autoscaling.module.alb.aws_lb.this[0]: Still creating... [40s elapsed]
module.database.aws_db_instance.database: Still creating... [40s elapsed]
module.autoscaling.module.alb.aws_lb.this[0]: Still creating... [50s elapsed]
module.database.aws_db_instance.database: Still creating... [50s elapsed]
module.autoscaling.module.alb.aws_lb.this[0]: Still creating... [1m0s elapsed]
module.database.aws_db_instance.database: Still creating... [1m0s elapsed]
module.autoscaling.module.alb.aws_lb.this[0]: Still creating... [1m10s elapsed]
module.database.aws_db_instance.database: Still creating... [1m10s elapsed]
module.autoscaling.module.alb.aws_lb.this[0]: Still creating... [1m20s elapsed]
module.database.aws_db_instance.database: Still creating... [1m20s elapsed]
module.autoscaling.module.alb.aws_lb.this[0]: Still creating... [1m30s elapsed]
module.database.aws_db_instance.database: Still creating... [1m30s elapsed]
module.database.aws_db_instance.database: Still creating... [1m40s elapsed]
module.autoscaling.module.alb.aws_lb.this[0]: Still creating... [1m40s elapsed]
module.autoscaling.module.alb.aws_lb.this[0]: Still creating... [1m50s elapsed]
module.database.aws_db_instance.database: Still creating... [1m50s elapsed]
module.autoscaling.module.alb.aws_lb.this[0]: Still creating... [2m0s elapsed]
module.database.aws_db_instance.database: Still creating... [2m0s elapsed]
module.database.aws_db_instance.database: Still creating... [2m10s elapsed]
module.autoscaling.module.alb.aws_lb.this[0]: Still creating... [2m10s elapsed]
module.autoscaling.module.alb.aws_lb.this[0]: Creation complete after 2m19s [id=arn:aws:elasticloadbalancing:us-west-2:878088820643:loadbalancer/app/my-3-tier-architecture/f7291cfbfbd5d7b8]
module.autoscaling.module.alb.aws_lb_target_group.main[0]: Creating...
module.database.aws_db_instance.database: Still creating... [2m20s elapsed]
module.autoscaling.module.alb.aws_lb_target_group.main[0]: Creation complete after 6s [id=arn:aws:elasticloadbalancing:us-west-2:878088820643:targetgroup/websvr20211209112919727800000007/1f5b25d1fdcbdece]
module.autoscaling.module.alb.aws_lb_listener.frontend_http_tcp[0]: Creating...
module.autoscaling.module.alb.aws_lb_listener.frontend_http_tcp[0]: Creation complete after 3s [id=arn:aws:elasticloadbalancing:us-west-2:878088820643:listener/app/my-3-tier-architecture/f7291cfbfbd5d7b8/ca1eb5cce3587811]
module.database.aws_db_instance.database: Still creating... [2m30s elapsed]
module.database.aws_db_instance.database: Still creating... [2m40s elapsed]
module.database.aws_db_instance.database: Still creating... [2m50s elapsed]
module.database.aws_db_instance.database: Still creating... [3m1s elapsed]
module.database.aws_db_instance.database: Still creating... [3m11s elapsed]
module.database.aws_db_instance.database: Still creating... [3m21s elapsed]
module.database.aws_db_instance.database: Still creating... [3m31s elapsed]
module.database.aws_db_instance.database: Still creating... [3m41s elapsed]
module.database.aws_db_instance.database: Still creating... [3m51s elapsed]
module.database.aws_db_instance.database: Still creating... [4m1s elapsed]
module.database.aws_db_instance.database: Still creating... [4m11s elapsed]
module.database.aws_db_instance.database: Still creating... [4m21s elapsed]
module.database.aws_db_instance.database: Still creating... [4m31s elapsed]
module.database.aws_db_instance.database: Still creating... [4m41s elapsed]
module.database.aws_db_instance.database: Creation complete after 4m42s [id=my-3-tier-architecture-db-instance]
module.autoscaling.data.cloudinit_config.config: Reading...
module.autoscaling.data.cloudinit_config.config: Read complete after 0s [id=624221325]
module.autoscaling.aws_launch_template.webserver: Creating...
module.autoscaling.aws_launch_template.webserver: Creation complete after 3s [id=lt-0cc886cecc984456f]
module.autoscaling.aws_autoscaling_group.webserver: Creating...
module.autoscaling.aws_autoscaling_group.webserver: Still creating... [10s elapsed]
module.autoscaling.aws_autoscaling_group.webserver: Still creating... [20s elapsed]
module.autoscaling.aws_autoscaling_group.webserver: Still creating... [30s elapsed]
module.autoscaling.aws_autoscaling_group.webserver: Still creating... [40s elapsed]
module.autoscaling.aws_autoscaling_group.webserver: Still creating... [50s elapsed]
module.autoscaling.aws_autoscaling_group.webserver: Still creating... [1m0s elapsed]
module.autoscaling.aws_autoscaling_group.webserver: Still creating... [1m10s elapsed]
module.autoscaling.aws_autoscaling_group.webserver: Still creating... [1m20s elapsed]
module.autoscaling.aws_autoscaling_group.webserver: Still creating... [1m30s elapsed]
module.autoscaling.aws_autoscaling_group.webserver: Still creating... [1m40s elapsed]
module.autoscaling.aws_autoscaling_group.webserver: Creation complete after 1m46s [id=my-3-tier-architecture-asg]

Apply complete! Resources: 40 added, 0 changed, 0 destroyed.

Outputs:

db_password = <sensitive>
lb_dns_name = "my-3-tier-architecture-220093037.us-west-2.elb.amazonaws.com"

Admin@DevOps MINGW64 ~/Desktop/test/3-tier-architecture (main)
$ ^C

Admin@DevOps MINGW64 ~/Desktop/test/3-tier-architecture (main)
$ terraform destroy
module.database.random_password.password: Refreshing state... [id=none]
module.autoscaling.module.iam_instance_profile.aws_iam_role.iam_role: Refreshing state... [id=terraform-20211209112432953600000001]
module.networking.module.vpc.aws_vpc.this[0]: Refreshing state... [id=vpc-0e41b88411b107ccb]
module.networking.module.vpc.aws_eip.nat[0]: Refreshing state... [id=eipalloc-0c271d80e0b96839c]
module.autoscaling.module.iam_instance_profile.aws_iam_role_policy.iam_role_policy: Refreshing state... [id=terraform-20211209112432953600000001:terraform-20211209112436676800000002]
module.autoscaling.module.iam_instance_profile.aws_iam_instance_profile.iam_instance_profile: Refreshing state... [id=terraform-20211209112436677900000003]
module.networking.module.vpc.aws_internet_gateway.this[0]: Refreshing state... [id=igw-0ef2ef5261f219c4a]
module.networking.module.lb_sg.aws_security_group.security_group: Refreshing state... [id=sg-0b7b411da05dccc53]
module.networking.module.vpc.aws_subnet.private[2]: Refreshing state... [id=subnet-0e0ef959cd3f6ec9a]
module.networking.module.vpc.aws_subnet.private[0]: Refreshing state... [id=subnet-0a21dbdfab358be99]
module.networking.module.vpc.aws_subnet.private[1]: Refreshing state... [id=subnet-098c5b2e22bec80c2]
module.networking.module.vpc.aws_subnet.public[0]: Refreshing state... [id=subnet-0b5d9b86e26d2bd6a]
module.networking.module.vpc.aws_subnet.public[2]: Refreshing state... [id=subnet-06ea4d30c5e2bda51]
module.networking.module.vpc.aws_subnet.database[2]: Refreshing state... [id=subnet-0925364cf17643020]
module.networking.module.vpc.aws_subnet.database[1]: Refreshing state... [id=subnet-0fa28647c54f6cb2b]
module.networking.module.vpc.aws_subnet.public[1]: Refreshing state... [id=subnet-0acce62e967c7df6c]
module.networking.module.vpc.aws_subnet.database[0]: Refreshing state... [id=subnet-04315cb26c7deb411]
module.networking.module.vpc.aws_route_table.public[0]: Refreshing state... [id=rtb-0ef7909133d8f121e]
module.networking.module.vpc.aws_route_table.private[0]: Refreshing state... [id=rtb-0441f7cbd2720da87]
module.networking.module.vpc.aws_nat_gateway.this[0]: Refreshing state... [id=nat-03484b3d7f6c31716]
module.networking.module.websvr_sg.aws_security_group.security_group: Refreshing state... [id=sg-0f7bb13cfc73fa728]
module.networking.module.vpc.aws_db_subnet_group.database[0]: Refreshing state... [id=my-3-tier-architecture-vpc]
module.networking.module.vpc.aws_route_table_association.public[1]: Refreshing state... [id=rtbassoc-0249675b9d2ada026]
module.networking.module.vpc.aws_route_table_association.public[0]: Refreshing state... [id=rtbassoc-0b8ffce252706c0bd]
module.networking.module.vpc.aws_route_table_association.public[2]: Refreshing state... [id=rtbassoc-006e03ba1bfe9ea3e]
module.networking.module.vpc.aws_route.public_internet_gateway[0]: Refreshing state... [id=r-rtb-0ef7909133d8f121e1080289494]
module.networking.module.vpc.aws_route_table_association.private[0]: Refreshing state... [id=rtbassoc-093ad37d7dbcc9617]
module.networking.module.vpc.aws_route_table_association.private[1]: Refreshing state... [id=rtbassoc-09b6e92be25ec25a5]
module.networking.module.vpc.aws_route_table_association.private[2]: Refreshing state... [id=rtbassoc-08e06733f874c2dc9]
module.networking.module.vpc.aws_route_table_association.database[0]: Refreshing state... [id=rtbassoc-056cda7f0ab4d0bd2]
module.networking.module.vpc.aws_route_table_association.database[1]: Refreshing state... [id=rtbassoc-07d45f374fe2558fa]
module.networking.module.vpc.aws_route_table_association.database[2]: Refreshing state... [id=rtbassoc-09b002cdbe4859874]
module.networking.module.vpc.aws_route.private_nat_gateway[0]: Refreshing state... [id=r-rtb-0441f7cbd2720da871080289494]
module.networking.module.db_sg.aws_security_group.security_group: Refreshing state... [id=sg-0b119588cc0bd9170]
module.database.aws_db_instance.database: Refreshing state... [id=my-3-tier-architecture-db-instance]
module.autoscaling.module.alb.aws_lb.this[0]: Refreshing state... [id=arn:aws:elasticloadbalancing:us-west-2:878088820643:loadbalancer/app/my-3-tier-architecture/f7291cfbfbd5d7b8]
module.autoscaling.aws_launch_template.webserver: Refreshing state... [id=lt-0cc886cecc984456f]
module.autoscaling.module.alb.aws_lb_target_group.main[0]: Refreshing state... [id=arn:aws:elasticloadbalancing:us-west-2:878088820643:targetgroup/websvr20211209112919727800000007/1f5b25d1fdcbdece]
module.autoscaling.module.alb.aws_lb_listener.frontend_http_tcp[0]: Refreshing state... [id=arn:aws:elasticloadbalancing:us-west-2:878088820643:listener/app/my-3-tier-architecture/f7291cfbfbd5d7b8/ca1eb5cce3587811]
module.autoscaling.aws_autoscaling_group.webserver: Refreshing state... [id=my-3-tier-architecture-asg]

Note: Objects have changed outside of Terraform

Terraform detected the following changes made outside of Terraform since the
last "terraform apply":

  # module.autoscaling.module.iam_instance_profile.aws_iam_role.iam_role has been changed
  ~ resource "aws_iam_role" "iam_role" {
        id                    = "terraform-20211209112432953600000001"
        name                  = "terraform-20211209112432953600000001"
      + tags                  = {}
        # (10 unchanged attributes hidden)

      - inline_policy {}
      + inline_policy {
          + name   = "terraform-20211209112436676800000002"
          + policy = jsonencode(
                {
                  + Statement = [
                      + {
                          + Action   = [
                              + "rds:*",
                              + "logs:*",
                            ]
                          + Effect   = "Allow"
                          + Resource = "*"
                          + Sid      = ""
                        },
                    ]
                  + Version   = "2012-10-17"
                }
            )
        }
    }
  # module.autoscaling.module.iam_instance_profile.aws_iam_instance_profile.iam_instance_profile has been changed
  ~ resource "aws_iam_instance_profile" "iam_instance_profile" {
        id          = "terraform-20211209112436677900000003"
        name        = "terraform-20211209112436677900000003"
      + tags        = {}
        # (6 unchanged attributes hidden)
    }
  # module.autoscaling.module.alb.aws_lb_listener.frontend_http_tcp[0] has been changed
  ~ resource "aws_lb_listener" "frontend_http_tcp" {
        id                = "arn:aws:elasticloadbalancing:us-west-2:878088820643:listener/app/my-3-tier-architecture/f7291cfbfbd5d7b8/ca1eb5cce3587811"
      + tags              = {}
        # (5 unchanged attributes hidden)

        # (1 unchanged block hidden)
    }
  # module.autoscaling.aws_autoscaling_group.webserver has been changed
  ~ resource "aws_autoscaling_group" "webserver" {
      + enabled_metrics           = []
        id                        = "my-3-tier-architecture-asg"
      + load_balancers            = []
        name                      = "my-3-tier-architecture-asg"
      + suspended_processes       = []
      + termination_policies      = []
        # (18 unchanged attributes hidden)

        # (1 unchanged block hidden)
    }
  # module.autoscaling.aws_launch_template.webserver has been changed
  ~ resource "aws_launch_template" "webserver" {
        id                      = "lt-0cc886cecc984456f"
        name                    = "my-3-tier-architecture20211209113143106400000008"
      + security_group_names    = []
      + tags                    = {}
        # (10 unchanged attributes hidden)

        # (1 unchanged block hidden)
    }
  # module.database.aws_db_instance.database has been changed
  ~ resource "aws_db_instance" "database" {
      + enabled_cloudwatch_logs_exports       = []
        id                                    = "my-3-tier-architecture-db-instance"
        name                                  = "pets"
      + security_group_names                  = []
      + tags                                  = {}
        # (54 unchanged attributes hidden)
    }
  # module.networking.module.lb_sg.aws_security_group.security_group has been changed
  ~ resource "aws_security_group" "security_group" {
        id                     = "sg-0b7b411da05dccc53"
        name                   = "terraform-20211209112449393700000004"
      + tags                   = {}
        # (9 unchanged attributes hidden)
    }
  # module.networking.module.db_sg.aws_security_group.security_group has been changed
  ~ resource "aws_security_group" "security_group" {
        id                     = "sg-0b119588cc0bd9170"
        name                   = "terraform-20211209112508982200000006"
      + tags                   = {}
        # (9 unchanged attributes hidden)
    }
  # module.networking.module.vpc.aws_route_table.public[0] has been changed
  ~ resource "aws_route_table" "public" {
        id               = "rtb-0ef7909133d8f121e"
      ~ route            = [
          + {
              + carrier_gateway_id         = ""
              + cidr_block                 = "0.0.0.0/0"
              + destination_prefix_list_id = ""
              + egress_only_gateway_id     = ""
              + gateway_id                 = "igw-0ef2ef5261f219c4a"
              + instance_id                = ""
              + ipv6_cidr_block            = ""
              + local_gateway_id           = ""
              + nat_gateway_id             = ""
              + network_interface_id       = ""
              + transit_gateway_id         = ""
              + vpc_endpoint_id            = ""
              + vpc_peering_connection_id  = ""
            },
        ]
        tags             = {
            "Name" = "my-3-tier-architecture-vpc-public"
        }
        # (5 unchanged attributes hidden)
    }
  # module.networking.module.vpc.aws_eip.nat[0] has been changed
  ~ resource "aws_eip" "nat" {
      + association_id       = "eipassoc-0319943e9b0ef4b3e"
        id                   = "eipalloc-0c271d80e0b96839c"
      + network_interface    = "eni-04a1f0ec77636c8f8"
      + private_dns          = "ip-10-0-101-111.us-west-2.compute.internal"
      + private_ip           = "10.0.101.111"
        tags                 = {
            "Name" = "my-3-tier-architecture-vpc-us-west-2a"
        }
        # (7 unchanged attributes hidden)
    }
  # module.networking.module.vpc.aws_route_table.private[0] has been changed
  ~ resource "aws_route_table" "private" {
        id               = "rtb-0441f7cbd2720da87"
      ~ route            = [
          + {
              + carrier_gateway_id         = ""
              + cidr_block                 = "0.0.0.0/0"
              + destination_prefix_list_id = ""
              + egress_only_gateway_id     = ""
              + gateway_id                 = ""
              + instance_id                = ""
              + ipv6_cidr_block            = ""
              + local_gateway_id           = ""
              + nat_gateway_id             = "nat-03484b3d7f6c31716"
              + network_interface_id       = ""
              + transit_gateway_id         = ""
              + vpc_endpoint_id            = ""
              + vpc_peering_connection_id  = ""
            },
        ]
        tags             = {
            "Name" = "my-3-tier-architecture-vpc-private"
        }
        # (5 unchanged attributes hidden)
    }
  # module.networking.module.websvr_sg.aws_security_group.security_group has been changed
  ~ resource "aws_security_group" "security_group" {
        id                     = "sg-0f7bb13cfc73fa728"
        name                   = "terraform-20211209112459071500000005"
      + tags                   = {}
        # (9 unchanged attributes hidden)
    }

Unless you have made equivalent changes to your configuration, or ignored the
relevant attributes using ignore_changes, the following plan may include
actions to undo or respond to these changes.

─────────────────────────────────────────────────────────────────────────────

Terraform used the selected providers to generate the following execution
plan. Resource actions are indicated with the following symbols:
  - destroy

Terraform will perform the following actions:

  # module.autoscaling.aws_autoscaling_group.webserver will be destroyed
  - resource "aws_autoscaling_group" "webserver" {
      - arn                       = "arn:aws:autoscaling:us-west-2:878088820643:autoScalingGroup:69a863f4-93ff-4914-8da6-0609e0df68de:autoScalingGroupName/my-3-tier-architecture-asg" -> null
      - availability_zones        = [
          - "us-west-2a",
          - "us-west-2b",
          - "us-west-2c",
        ] -> null
      - capacity_rebalance        = false -> null
      - default_cooldown          = 300 -> null
      - desired_capacity          = 1 -> null
      - enabled_metrics           = [] -> null
      - force_delete              = false -> null
      - force_delete_warm_pool    = false -> null
      - health_check_grace_period = 300 -> null
      - health_check_type         = "EC2" -> null
      - id                        = "my-3-tier-architecture-asg" -> null
      - load_balancers            = [] -> null
      - max_instance_lifetime     = 0 -> null
      - max_size                  = 3 -> null
      - metrics_granularity       = "1Minute" -> null
      - min_size                  = 1 -> null
      - name                      = "my-3-tier-architecture-asg" -> null
      - protect_from_scale_in     = false -> null
      - service_linked_role_arn   = "arn:aws:iam::878088820643:role/aws-service-role/autoscaling.amazonaws.com/AWSServiceRoleForAutoScaling" -> null
      - suspended_processes       = [] -> null
      - target_group_arns         = [
          - "arn:aws:elasticloadbalancing:us-west-2:878088820643:targetgroup/websvr20211209112919727800000007/1f5b25d1fdcbdece",
        ] -> null
      - termination_policies      = [] -> null
      - vpc_zone_identifier       = [
          - "subnet-098c5b2e22bec80c2",
          - "subnet-0a21dbdfab358be99",
          - "subnet-0e0ef959cd3f6ec9a",
        ] -> null
      - wait_for_capacity_timeout = "10m" -> null

      - launch_template {
          - id      = "lt-0cc886cecc984456f" -> null
          - name    = "my-3-tier-architecture20211209113143106400000008" -> null
          - version = "1" -> null
        }
    }

  # module.autoscaling.aws_launch_template.webserver will be destroyed
  - resource "aws_launch_template" "webserver" {
      - arn                     = "arn:aws:ec2:us-west-2:878088820643:launch-template/lt-0cc886cecc984456f" -> null
      - default_version         = 1 -> null
      - disable_api_termination = false -> null
      - id                      = "lt-0cc886cecc984456f" -> null
      - image_id                = "ami-074251216af698218" -> null
      - instance_type           = "t2.micro" -> null
      - latest_version          = 1 -> null
      - name                    = "my-3-tier-architecture20211209113143106400000008" -> null
      - name_prefix             = "my-3-tier-architecture" -> null
      - security_group_names    = [] -> null
      - tags                    = {} -> null
      - tags_all                = {} -> null
      - user_data               = "H4sIAAAAAAAA/2SSTW/UMBCG75HyH0bmipMtWxVhxIGPSiBRkFBLQQhVjj2769ax3ZlJ0y3lv6Ow/di2OcT2vI/nHXnmfU6CSfThuqCBfogSiiVp+3CJ/jV0eUje0vqNOvh0sP/u69GXD2+//VTVdNLfkTjkZGCnmdVVXWm9DdXVXW6yiRdIej+57ENaGnjZBdkC/psLXkrrYh68djktwrKuDkKPT2yePWRGCoInixCRTV0BaAAoVlYGWhTXMtIFUjPRkzp9eUxIBihnMdPvNl6Q+sCTFxtQs73dXXUruU2lBq5vIwB/7rcAamAkZQCU9X1I6vkDsVjmMZNXBtRxxFeHPy7s7Gh+XHZXHx+h3ortLOOEFhR+JCeUmN0k9ms91xKQtCW3CoJOBkLtOx0Si00OG7cuiRaLve4y7jQD6xFZ9IuGPDe2t1c52ZEbl3szn8/21L3P37qiIbne3zyoGyiC5s+wEils2taW0CyDrIZuut4SlswtuywyhnQWkdoLm0KMVo/YbTqgmVxLGNEychutIAtcw+k5aALVWGYU/vW76SiPjHTi85hitv5koKjgGsYlCujzABo2RQ3pKhTwWGJe95ikuQplozTtffSm/3VVrDuzy7sZOT3frFPa7XxP51jruvoXAAD///g6zXEmAwAA" -> null
      - vpc_security_group_ids  = [
          - "sg-0f7bb13cfc73fa728",
        ] -> null

      - iam_instance_profile {
          - name = "terraform-20211209112436677900000003" -> null
        }
    }

  # module.database.aws_db_instance.database will be destroyed
  - resource "aws_db_instance" "database" {
      - address                               = "my-3-tier-architecture-db-instance.cypnrff6bxl1.us-west-2.rds.amazonaws.com" -> null
      - allocated_storage                     = 10 -> null
      - arn                                   = "arn:aws:rds:us-west-2:878088820643:db:my-3-tier-architecture-db-instance" -> null
      - auto_minor_version_upgrade            = true -> null
      - availability_zone                     = "us-west-2a" -> null
      - backup_retention_period               = 0 -> null
      - backup_window                         = "08:28-08:58" -> null
      - ca_cert_identifier                    = "rds-ca-2019" -> null
      - character_set_name                    = "" -> null
      - copy_tags_to_snapshot                 = false -> null
      - customer_owned_ip_enabled             = false -> null
      - db_subnet_group_name                  = "my-3-tier-architecture-vpc" -> null
      - delete_automated_backups              = true -> null
      - deletion_protection                   = false -> null
      - domain                                = "" -> null
      - domain_iam_role_name                  = "" -> null
      - enabled_cloudwatch_logs_exports       = [] -> null
      - endpoint                              = "my-3-tier-architecture-db-instance.cypnrff6bxl1.us-west-2.rds.amazonaws.com:3306" -> null
      - engine                                = "mysql" -> null
      - engine_version                        = "8.0" -> null
      - engine_version_actual                 = "8.0.23" -> null
      - hosted_zone_id                        = "Z1PVIF0B656C1W" -> null
      - iam_database_authentication_enabled   = false -> null
      - id                                    = "my-3-tier-architecture-db-instance" -> null
      - identifier                            = "my-3-tier-architecture-db-instance" -> null
      - instance_class                        = "db.t2.micro" -> null
      - iops                                  = 0 -> null
      - kms_key_id                            = "" -> null
      - latest_restorable_time                = "0001-01-01T00:00:00Z" -> null
      - license_model                         = "general-public-license" -> null
      - maintenance_window                    = "sun:06:14-sun:06:44" -> null
      - max_allocated_storage                 = 0 -> null
      - monitoring_interval                   = 0 -> null
      - monitoring_role_arn                   = "" -> null
      - multi_az                              = false -> null
      - name                                  = "pets" -> null
      - nchar_character_set_name              = "" -> null
      - option_group_name                     = "default:mysql-8-0" -> null
      - parameter_group_name                  = "default.mysql8.0" -> null
      - password                              = (sensitive value)
      - performance_insights_enabled          = false -> null
      - performance_insights_kms_key_id       = "" -> null
      - performance_insights_retention_period = 0 -> null
      - port                                  = 3306 -> null
      - publicly_accessible                   = false -> null
      - replica_mode                          = "" -> null
      - replicas                              = [] -> null
      - replicate_source_db                   = "" -> null
      - resource_id                           = "db-PT63CGC72IMFQUHGVBPPZBIOIQ" -> null
      - security_group_names                  = [] -> null
      - skip_final_snapshot                   = true -> null
      - status                                = "available" -> null
      - storage_encrypted                     = false -> null
      - storage_type                          = "gp2" -> null
      - tags                                  = {} -> null
      - tags_all                              = {} -> null
      - timezone                              = "" -> null
      - username                              = "admin" -> null
      - vpc_security_group_ids                = [
          - "sg-0b119588cc0bd9170",
        ] -> null
    }

  # module.database.random_password.password will be destroyed
  - resource "random_password" "password" {
      - id               = "none" -> null
      - length           = 16 -> null
      - lower            = true -> null
      - min_lower        = 0 -> null
      - min_numeric      = 0 -> null
      - min_special      = 0 -> null
      - min_upper        = 0 -> null
      - number           = true -> null
      - override_special = "_%@/'\"" -> null
      - result           = (sensitive value)
      - special          = true -> null
      - upper            = true -> null
    }

  # module.autoscaling.module.alb.aws_lb.this[0] will be destroyed
  - resource "aws_lb" "this" {
      - arn                        = "arn:aws:elasticloadbalancing:us-west-2:878088820643:loadbalancer/app/my-3-tier-architecture/f7291cfbfbd5d7b8" -> null
      - arn_suffix                 = "app/my-3-tier-architecture/f7291cfbfbd5d7b8" -> null
      - dns_name                   = "my-3-tier-architecture-220093037.us-west-2.elb.amazonaws.com" -> null
      - drop_invalid_header_fields = false -> null
      - enable_deletion_protection = false -> null
      - enable_http2               = true -> null
      - id                         = "arn:aws:elasticloadbalancing:us-west-2:878088820643:loadbalancer/app/my-3-tier-architecture/f7291cfbfbd5d7b8" -> null
      - idle_timeout               = 60 -> null
      - internal                   = false -> null
      - ip_address_type            = "ipv4" -> null
      - load_balancer_type         = "application" -> null
      - name                       = "my-3-tier-architecture" -> null
      - security_groups            = [
          - "sg-0b7b411da05dccc53",
        ] -> null
      - subnets                    = [
          - "subnet-06ea4d30c5e2bda51",
          - "subnet-0acce62e967c7df6c",
          - "subnet-0b5d9b86e26d2bd6a",
        ] -> null
      - tags                       = {
          - "Name" = "my-3-tier-architecture"
        } -> null
      - tags_all                   = {
          - "Name" = "my-3-tier-architecture"
        } -> null
      - vpc_id                     = "vpc-0e41b88411b107ccb" -> null
      - zone_id                    = "Z1H1FL5HABSF5" -> null

      - access_logs {
          - enabled = false -> null
        }

      - subnet_mapping {
          - subnet_id = "subnet-06ea4d30c5e2bda51" -> null
        }
      - subnet_mapping {
          - subnet_id = "subnet-0acce62e967c7df6c" -> null
        }
      - subnet_mapping {
          - subnet_id = "subnet-0b5d9b86e26d2bd6a" -> null
        }

      - timeouts {
          - create = "10m" -> null
          - delete = "10m" -> null
          - update = "10m" -> null
        }
    }

  # module.autoscaling.module.alb.aws_lb_listener.frontend_http_tcp[0] will be destroyed
  - resource "aws_lb_listener" "frontend_http_tcp" {
      - arn               = "arn:aws:elasticloadbalancing:us-west-2:878088820643:listener/app/my-3-tier-architecture/f7291cfbfbd5d7b8/ca1eb5cce3587811" -> null
      - id                = "arn:aws:elasticloadbalancing:us-west-2:878088820643:listener/app/my-3-tier-architecture/f7291cfbfbd5d7b8/ca1eb5cce3587811" -> null
      - load_balancer_arn = "arn:aws:elasticloadbalancing:us-west-2:878088820643:loadbalancer/app/my-3-tier-architecture/f7291cfbfbd5d7b8" -> null
      - port              = 80 -> null
      - protocol          = "HTTP" -> null
      - tags              = {} -> null
      - tags_all          = {} -> null

      - default_action {
          - order            = 1 -> null
          - target_group_arn = "arn:aws:elasticloadbalancing:us-west-2:878088820643:targetgroup/websvr20211209112919727800000007/1f5b25d1fdcbdece" -> null
          - type             = "forward" -> null
        }
    }

  # module.autoscaling.module.alb.aws_lb_target_group.main[0] will be destroyed
  - resource "aws_lb_target_group" "main" {
      - arn                                = "arn:aws:elasticloadbalancing:us-west-2:878088820643:targetgroup/websvr20211209112919727800000007/1f5b25d1fdcbdece" -> null
      - arn_suffix                         = "targetgroup/websvr20211209112919727800000007/1f5b25d1fdcbdece" -> null
      - deregistration_delay               = "300" -> null
      - id                                 = "arn:aws:elasticloadbalancing:us-west-2:878088820643:targetgroup/websvr20211209112919727800000007/1f5b25d1fdcbdece" -> null
      - lambda_multi_value_headers_enabled = false -> null
      - load_balancing_algorithm_type      = "round_robin" -> null
      - name                               = "websvr20211209112919727800000007" -> null
      - name_prefix                        = "websvr" -> null
      - port                               = 8080 -> null
      - protocol                           = "HTTP" -> null
      - protocol_version                   = "HTTP1" -> null
      - proxy_protocol_v2                  = false -> null
      - slow_start                         = 0 -> null
      - tags                               = {
          - "Name" = "websvr"
        } -> null
      - tags_all                           = {
          - "Name" = "websvr"
        } -> null
      - target_type                        = "instance" -> null
      - vpc_id                             = "vpc-0e41b88411b107ccb" -> null

      - health_check {
          - enabled             = true -> null
          - healthy_threshold   = 5 -> null
          - interval            = 30 -> null
          - matcher             = "200" -> null
          - path                = "/" -> null
          - port                = "traffic-port" -> null
          - protocol            = "HTTP" -> null
          - timeout             = 5 -> null
          - unhealthy_threshold = 2 -> null
        }

      - stickiness {
          - cookie_duration = 86400 -> null
          - enabled         = false -> null
          - type            = "lb_cookie" -> null
        }
    }

  # module.autoscaling.module.iam_instance_profile.aws_iam_instance_profile.iam_instance_profile will be destroyed
  - resource "aws_iam_instance_profile" "iam_instance_profile" {
      - arn         = "arn:aws:iam::878088820643:instance-profile/terraform-20211209112436677900000003" -> null
      - create_date = "2021-12-09T11:24:38Z" -> null
      - id          = "terraform-20211209112436677900000003" -> null
      - name        = "terraform-20211209112436677900000003" -> null
      - path        = "/" -> null
      - role        = "terraform-20211209112432953600000001" -> null
      - tags        = {} -> null
      - tags_all    = {} -> null
      - unique_id   = "AIPA4Y4RMC6R5OF7FYSP4" -> null
    }

  # module.autoscaling.module.iam_instance_profile.aws_iam_role.iam_role will be destroyed
  - resource "aws_iam_role" "iam_role" {
      - arn                   = "arn:aws:iam::878088820643:role/terraform-20211209112432953600000001" -> null
      - assume_role_policy    = jsonencode(
            {
              - Statement = [
                  - {
                      - Action    = "sts:AssumeRole"
                      - Effect    = "Allow"
                      - Principal = {
                          - Service = "ec2.amazonaws.com"
                        }
                    },
                ]
              - Version   = "2012-10-17"
            }
        ) -> null
      - create_date           = "2021-12-09T11:24:34Z" -> null
      - force_detach_policies = false -> null
      - id                    = "terraform-20211209112432953600000001" -> null
      - managed_policy_arns   = [] -> null
      - max_session_duration  = 3600 -> null
      - name                  = "terraform-20211209112432953600000001" -> null
      - name_prefix           = "terraform-" -> null
      - path                  = "/" -> null
      - tags                  = {} -> null
      - tags_all              = {} -> null
      - unique_id             = "AROA4Y4RMC6RYN65VDLFM" -> null

      - inline_policy {
          - name   = "terraform-20211209112436676800000002" -> null
          - policy = jsonencode(
                {
                  - Statement = [
                      - {
                          - Action   = [
                              - "rds:*",
                              - "logs:*",
                            ]
                          - Effect   = "Allow"
                          - Resource = "*"
                          - Sid      = ""
                        },
                    ]
                  - Version   = "2012-10-17"
                }
            ) -> null
        }
    }

  # module.autoscaling.module.iam_instance_profile.aws_iam_role_policy.iam_role_policy will be destroyed
  - resource "aws_iam_role_policy" "iam_role_policy" {
      - id     = "terraform-20211209112432953600000001:terraform-20211209112436676800000002" -> null
      - name   = "terraform-20211209112436676800000002" -> null
      - policy = jsonencode(
            {
              - Statement = [
                  - {
                      - Action   = [
                          - "rds:*",
                          - "logs:*",
                        ]
                      - Effect   = "Allow"
                      - Resource = "*"
                      - Sid      = ""
                    },
                ]
              - Version   = "2012-10-17"
            }
        ) -> null
      - role   = "terraform-20211209112432953600000001" -> null
    }

  # module.networking.module.db_sg.aws_security_group.security_group will be destroyed
  - resource "aws_security_group" "security_group" {
      - arn                    = "arn:aws:ec2:us-west-2:878088820643:security-group/sg-0b119588cc0bd9170" -> null
      - description            = "Managed by Terraform" -> null
      - egress                 = [
          - {
              - cidr_blocks      = [
                  - "0.0.0.0/0",
                ]
              - description      = ""
              - from_port        = 0
              - ipv6_cidr_blocks = []
              - prefix_list_ids  = []
              - protocol         = "-1"
              - security_groups  = []
              - self             = false
              - to_port          = 0
            },
        ] -> null
      - id                     = "sg-0b119588cc0bd9170" -> null
      - ingress                = [
          - {
              - cidr_blocks      = []
              - description      = ""
              - from_port        = 0
              - ipv6_cidr_blocks = []
              - prefix_list_ids  = []
              - protocol         = "-1"
              - security_groups  = []
              - self             = true
              - to_port          = 0
            },
          - {
              - cidr_blocks      = []
              - description      = ""
              - from_port        = 3306
              - ipv6_cidr_blocks = []
              - prefix_list_ids  = []
              - protocol         = "tcp"
              - security_groups  = [
                  - "sg-0f7bb13cfc73fa728",
                ]
              - self             = false
              - to_port          = 3306
            },
        ] -> null
      - name                   = "terraform-20211209112508982200000006" -> null
      - name_prefix            = "terraform-" -> null
      - owner_id               = "878088820643" -> null
      - revoke_rules_on_delete = false -> null
      - tags                   = {} -> null
      - tags_all               = {} -> null
      - vpc_id                 = "vpc-0e41b88411b107ccb" -> null
    }

  # module.networking.module.lb_sg.aws_security_group.security_group will be destroyed
  - resource "aws_security_group" "security_group" {
      - arn                    = "arn:aws:ec2:us-west-2:878088820643:security-group/sg-0b7b411da05dccc53" -> null
      - description            = "Managed by Terraform" -> null
      - egress                 = [
          - {
              - cidr_blocks      = [
                  - "0.0.0.0/0",
                ]
              - description      = ""
              - from_port        = 0
              - ipv6_cidr_blocks = []
              - prefix_list_ids  = []
              - protocol         = "-1"
              - security_groups  = []
              - self             = false
              - to_port          = 0
            },
        ] -> null
      - id                     = "sg-0b7b411da05dccc53" -> null
      - ingress                = [
          - {
              - cidr_blocks      = [
                  - "0.0.0.0/0",
                ]
              - description      = ""
              - from_port        = 80
              - ipv6_cidr_blocks = []
              - prefix_list_ids  = []
              - protocol         = "tcp"
              - security_groups  = []
              - self             = false
              - to_port          = 80
            },
          - {
              - cidr_blocks      = []
              - description      = ""
              - from_port        = 0
              - ipv6_cidr_blocks = []
              - prefix_list_ids  = []
              - protocol         = "-1"
              - security_groups  = []
              - self             = true
              - to_port          = 0
            },
        ] -> null
      - name                   = "terraform-20211209112449393700000004" -> null
      - name_prefix            = "terraform-" -> null
      - owner_id               = "878088820643" -> null
      - revoke_rules_on_delete = false -> null
      - tags                   = {} -> null
      - tags_all               = {} -> null
      - vpc_id                 = "vpc-0e41b88411b107ccb" -> null
    }

  # module.networking.module.vpc.aws_db_subnet_group.database[0] will be destroyed
  - resource "aws_db_subnet_group" "database" {
      - arn         = "arn:aws:rds:us-west-2:878088820643:subgrp:my-3-tier-architecture-vpc" -> null
      - description = "Database subnet group for my-3-tier-architecture-vpc" -> null
      - id          = "my-3-tier-architecture-vpc" -> null
      - name        = "my-3-tier-architecture-vpc" -> null
      - subnet_ids  = [
          - "subnet-04315cb26c7deb411",
          - "subnet-0925364cf17643020",
          - "subnet-0fa28647c54f6cb2b",
        ] -> null
      - tags        = {
          - "Name" = "my-3-tier-architecture-vpc"
        } -> null
      - tags_all    = {
          - "Name" = "my-3-tier-architecture-vpc"
        } -> null
    }

  # module.networking.module.vpc.aws_eip.nat[0] will be destroyed
  - resource "aws_eip" "nat" {
      - association_id       = "eipassoc-0319943e9b0ef4b3e" -> null
      - domain               = "vpc" -> null
      - id                   = "eipalloc-0c271d80e0b96839c" -> null
      - network_border_group = "us-west-2" -> null
      - network_interface    = "eni-04a1f0ec77636c8f8" -> null
      - private_dns          = "ip-10-0-101-111.us-west-2.compute.internal" -> null
      - private_ip           = "10.0.101.111" -> null
      - public_dns           = "ec2-54-71-163-248.us-west-2.compute.amazonaws.com" -> null
      - public_ip            = "54.71.163.248" -> null
      - public_ipv4_pool     = "amazon" -> null
      - tags                 = {
          - "Name" = "my-3-tier-architecture-vpc-us-west-2a"
        } -> null
      - tags_all             = {
          - "Name" = "my-3-tier-architecture-vpc-us-west-2a"
        } -> null
      - vpc                  = true -> null
    }

  # module.networking.module.vpc.aws_internet_gateway.this[0] will be destroyed
  - resource "aws_internet_gateway" "this" {
      - arn      = "arn:aws:ec2:us-west-2:878088820643:internet-gateway/igw-0ef2ef5261f219c4a" -> null
      - id       = "igw-0ef2ef5261f219c4a" -> null
      - owner_id = "878088820643" -> null
      - tags     = {
          - "Name" = "my-3-tier-architecture-vpc"
        } -> null
      - tags_all = {
          - "Name" = "my-3-tier-architecture-vpc"
        } -> null
      - vpc_id   = "vpc-0e41b88411b107ccb" -> null
    }

  # module.networking.module.vpc.aws_nat_gateway.this[0] will be destroyed
  - resource "aws_nat_gateway" "this" {
      - allocation_id        = "eipalloc-0c271d80e0b96839c" -> null
      - connectivity_type    = "public" -> null
      - id                   = "nat-03484b3d7f6c31716" -> null
      - network_interface_id = "eni-04a1f0ec77636c8f8" -> null
      - private_ip           = "10.0.101.111" -> null
      - public_ip            = "54.71.163.248" -> null
      - subnet_id            = "subnet-0b5d9b86e26d2bd6a" -> null
      - tags                 = {
          - "Name" = "my-3-tier-architecture-vpc-us-west-2a"
        } -> null
      - tags_all             = {
          - "Name" = "my-3-tier-architecture-vpc-us-west-2a"
        } -> null
    }

  # module.networking.module.vpc.aws_route.private_nat_gateway[0] will be destroyed
  - resource "aws_route" "private_nat_gateway" {
      - destination_cidr_block = "0.0.0.0/0" -> null
      - id                     = "r-rtb-0441f7cbd2720da871080289494" -> null
      - nat_gateway_id         = "nat-03484b3d7f6c31716" -> null
      - origin                 = "CreateRoute" -> null
      - route_table_id         = "rtb-0441f7cbd2720da87" -> null
      - state                  = "active" -> null

      - timeouts {
          - create = "5m" -> null
        }
    }

  # module.networking.module.vpc.aws_route.public_internet_gateway[0] will be destroyed
  - resource "aws_route" "public_internet_gateway" {
      - destination_cidr_block = "0.0.0.0/0" -> null
      - gateway_id             = "igw-0ef2ef5261f219c4a" -> null
      - id                     = "r-rtb-0ef7909133d8f121e1080289494" -> null
      - origin                 = "CreateRoute" -> null
      - route_table_id         = "rtb-0ef7909133d8f121e" -> null
      - state                  = "active" -> null

      - timeouts {
          - create = "5m" -> null
        }
    }

  # module.networking.module.vpc.aws_route_table.private[0] will be destroyed
  - resource "aws_route_table" "private" {
      - arn              = "arn:aws:ec2:us-west-2:878088820643:route-table/rtb-0441f7cbd2720da87" -> null
      - id               = "rtb-0441f7cbd2720da87" -> null
      - owner_id         = "878088820643" -> null
      - propagating_vgws = [] -> null
      - route            = [
          - {
              - carrier_gateway_id         = ""
              - cidr_block                 = "0.0.0.0/0"
              - destination_prefix_list_id = ""
              - egress_only_gateway_id     = ""
              - gateway_id                 = ""
              - instance_id                = ""
              - ipv6_cidr_block            = ""
              - local_gateway_id           = ""
              - nat_gateway_id             = "nat-03484b3d7f6c31716"
              - network_interface_id       = ""
              - transit_gateway_id         = ""
              - vpc_endpoint_id            = ""
              - vpc_peering_connection_id  = ""
            },
        ] -> null
      - tags             = {
          - "Name" = "my-3-tier-architecture-vpc-private"
        } -> null
      - tags_all         = {
          - "Name" = "my-3-tier-architecture-vpc-private"
        } -> null
      - vpc_id           = "vpc-0e41b88411b107ccb" -> null
    }

  # module.networking.module.vpc.aws_route_table.public[0] will be destroyed
  - resource "aws_route_table" "public" {
      - arn              = "arn:aws:ec2:us-west-2:878088820643:route-table/rtb-0ef7909133d8f121e" -> null
      - id               = "rtb-0ef7909133d8f121e" -> null
      - owner_id         = "878088820643" -> null
      - propagating_vgws = [] -> null
      - route            = [
          - {
              - carrier_gateway_id         = ""
              - cidr_block                 = "0.0.0.0/0"
              - destination_prefix_list_id = ""
              - egress_only_gateway_id     = ""
              - gateway_id                 = "igw-0ef2ef5261f219c4a"
              - instance_id                = ""
              - ipv6_cidr_block            = ""
              - local_gateway_id           = ""
              - nat_gateway_id             = ""
              - network_interface_id       = ""
              - transit_gateway_id         = ""
              - vpc_endpoint_id            = ""
              - vpc_peering_connection_id  = ""
            },
        ] -> null
      - tags             = {
          - "Name" = "my-3-tier-architecture-vpc-public"
        } -> null
      - tags_all         = {
          - "Name" = "my-3-tier-architecture-vpc-public"
        } -> null
      - vpc_id           = "vpc-0e41b88411b107ccb" -> null
    }

  # module.networking.module.vpc.aws_route_table_association.database[0] will be destroyed
  - resource "aws_route_table_association" "database" {
      - id             = "rtbassoc-056cda7f0ab4d0bd2" -> null
      - route_table_id = "rtb-0441f7cbd2720da87" -> null
      - subnet_id      = "subnet-04315cb26c7deb411" -> null
    }

  # module.networking.module.vpc.aws_route_table_association.database[1] will be destroyed
  - resource "aws_route_table_association" "database" {
      - id             = "rtbassoc-07d45f374fe2558fa" -> null
      - route_table_id = "rtb-0441f7cbd2720da87" -> null
      - subnet_id      = "subnet-0fa28647c54f6cb2b" -> null
    }

  # module.networking.module.vpc.aws_route_table_association.database[2] will be destroyed
  - resource "aws_route_table_association" "database" {
      - id             = "rtbassoc-09b002cdbe4859874" -> null
      - route_table_id = "rtb-0441f7cbd2720da87" -> null
      - subnet_id      = "subnet-0925364cf17643020" -> null
    }

  # module.networking.module.vpc.aws_route_table_association.private[0] will be destroyed
  - resource "aws_route_table_association" "private" {
      - id             = "rtbassoc-093ad37d7dbcc9617" -> null
      - route_table_id = "rtb-0441f7cbd2720da87" -> null
      - subnet_id      = "subnet-0a21dbdfab358be99" -> null
    }

  # module.networking.module.vpc.aws_route_table_association.private[1] will be destroyed
  - resource "aws_route_table_association" "private" {
      - id             = "rtbassoc-09b6e92be25ec25a5" -> null
      - route_table_id = "rtb-0441f7cbd2720da87" -> null
      - subnet_id      = "subnet-098c5b2e22bec80c2" -> null
    }

  # module.networking.module.vpc.aws_route_table_association.private[2] will be destroyed
  - resource "aws_route_table_association" "private" {
      - id             = "rtbassoc-08e06733f874c2dc9" -> null
      - route_table_id = "rtb-0441f7cbd2720da87" -> null
      - subnet_id      = "subnet-0e0ef959cd3f6ec9a" -> null
    }

  # module.networking.module.vpc.aws_route_table_association.public[0] will be destroyed
  - resource "aws_route_table_association" "public" {
      - id             = "rtbassoc-0b8ffce252706c0bd" -> null
      - route_table_id = "rtb-0ef7909133d8f121e" -> null
      - subnet_id      = "subnet-0b5d9b86e26d2bd6a" -> null
    }

  # module.networking.module.vpc.aws_route_table_association.public[1] will be destroyed
  - resource "aws_route_table_association" "public" {
      - id             = "rtbassoc-0249675b9d2ada026" -> null
      - route_table_id = "rtb-0ef7909133d8f121e" -> null
      - subnet_id      = "subnet-0acce62e967c7df6c" -> null
    }

  # module.networking.module.vpc.aws_route_table_association.public[2] will be destroyed
  - resource "aws_route_table_association" "public" {
      - id             = "rtbassoc-006e03ba1bfe9ea3e" -> null
      - route_table_id = "rtb-0ef7909133d8f121e" -> null
      - subnet_id      = "subnet-06ea4d30c5e2bda51" -> null
    }

  # module.networking.module.vpc.aws_subnet.database[0] will be destroyed
  - resource "aws_subnet" "database" {
      - arn                             = "arn:aws:ec2:us-west-2:878088820643:subnet/subnet-04315cb26c7deb411" -> null
      - assign_ipv6_address_on_creation = false -> null
      - availability_zone               = "us-west-2a" -> null
      - availability_zone_id            = "usw2-az1" -> null
      - cidr_block                      = "10.0.21.0/24" -> null
      - id                              = "subnet-04315cb26c7deb411" -> null
      - map_customer_owned_ip_on_launch = false -> null
      - map_public_ip_on_launch         = false -> null
      - owner_id                        = "878088820643" -> null
      - tags                            = {
          - "Name" = "my-3-tier-architecture-vpc-db-us-west-2a"
        } -> null
      - tags_all                        = {
          - "Name" = "my-3-tier-architecture-vpc-db-us-west-2a"
        } -> null
      - vpc_id                          = "vpc-0e41b88411b107ccb" -> null
    }

  # module.networking.module.vpc.aws_subnet.database[1] will be destroyed
  - resource "aws_subnet" "database" {
      - arn                             = "arn:aws:ec2:us-west-2:878088820643:subnet/subnet-0fa28647c54f6cb2b" -> null
      - assign_ipv6_address_on_creation = false -> null
      - availability_zone               = "us-west-2b" -> null
      - availability_zone_id            = "usw2-az2" -> null
      - cidr_block                      = "10.0.22.0/24" -> null
      - id                              = "subnet-0fa28647c54f6cb2b" -> null
      - map_customer_owned_ip_on_launch = false -> null
      - map_public_ip_on_launch         = false -> null
      - owner_id                        = "878088820643" -> null
      - tags                            = {
          - "Name" = "my-3-tier-architecture-vpc-db-us-west-2b"
        } -> null
      - tags_all                        = {
          - "Name" = "my-3-tier-architecture-vpc-db-us-west-2b"
        } -> null
      - vpc_id                          = "vpc-0e41b88411b107ccb" -> null
    }

  # module.networking.module.vpc.aws_subnet.database[2] will be destroyed
  - resource "aws_subnet" "database" {
      - arn                             = "arn:aws:ec2:us-west-2:878088820643:subnet/subnet-0925364cf17643020" -> null
      - assign_ipv6_address_on_creation = false -> null
      - availability_zone               = "us-west-2c" -> null
      - availability_zone_id            = "usw2-az3" -> null
      - cidr_block                      = "10.0.23.0/24" -> null
      - id                              = "subnet-0925364cf17643020" -> null
      - map_customer_owned_ip_on_launch = false -> null
      - map_public_ip_on_launch         = false -> null
      - owner_id                        = "878088820643" -> null
      - tags                            = {
          - "Name" = "my-3-tier-architecture-vpc-db-us-west-2c"
        } -> null
      - tags_all                        = {
          - "Name" = "my-3-tier-architecture-vpc-db-us-west-2c"
        } -> null
      - vpc_id                          = "vpc-0e41b88411b107ccb" -> null
    }

  # module.networking.module.vpc.aws_subnet.private[0] will be destroyed
  - resource "aws_subnet" "private" {
      - arn                             = "arn:aws:ec2:us-west-2:878088820643:subnet/subnet-0a21dbdfab358be99" -> null
      - assign_ipv6_address_on_creation = false -> null
      - availability_zone               = "us-west-2a" -> null
      - availability_zone_id            = "usw2-az1" -> null
      - cidr_block                      = "10.0.1.0/24" -> null
      - id                              = "subnet-0a21dbdfab358be99" -> null
      - map_customer_owned_ip_on_launch = false -> null
      - map_public_ip_on_launch         = false -> null
      - owner_id                        = "878088820643" -> null
      - tags                            = {
          - "Name" = "my-3-tier-architecture-vpc-private-us-west-2a"
        } -> null
      - tags_all                        = {
          - "Name" = "my-3-tier-architecture-vpc-private-us-west-2a"
        } -> null
      - vpc_id                          = "vpc-0e41b88411b107ccb" -> null
    }

  # module.networking.module.vpc.aws_subnet.private[1] will be destroyed
  - resource "aws_subnet" "private" {
      - arn                             = "arn:aws:ec2:us-west-2:878088820643:subnet/subnet-098c5b2e22bec80c2" -> null
      - assign_ipv6_address_on_creation = false -> null
      - availability_zone               = "us-west-2b" -> null
      - availability_zone_id            = "usw2-az2" -> null
      - cidr_block                      = "10.0.2.0/24" -> null
      - id                              = "subnet-098c5b2e22bec80c2" -> null
      - map_customer_owned_ip_on_launch = false -> null
      - map_public_ip_on_launch         = false -> null
      - owner_id                        = "878088820643" -> null
      - tags                            = {
          - "Name" = "my-3-tier-architecture-vpc-private-us-west-2b"
        } -> null
      - tags_all                        = {
          - "Name" = "my-3-tier-architecture-vpc-private-us-west-2b"
        } -> null
      - vpc_id                          = "vpc-0e41b88411b107ccb" -> null
    }

  # module.networking.module.vpc.aws_subnet.private[2] will be destroyed
  - resource "aws_subnet" "private" {
      - arn                             = "arn:aws:ec2:us-west-2:878088820643:subnet/subnet-0e0ef959cd3f6ec9a" -> null
      - assign_ipv6_address_on_creation = false -> null
      - availability_zone               = "us-west-2c" -> null
      - availability_zone_id            = "usw2-az3" -> null
      - cidr_block                      = "10.0.3.0/24" -> null
      - id                              = "subnet-0e0ef959cd3f6ec9a" -> null
      - map_customer_owned_ip_on_launch = false -> null
      - map_public_ip_on_launch         = false -> null
      - owner_id                        = "878088820643" -> null
      - tags                            = {
          - "Name" = "my-3-tier-architecture-vpc-private-us-west-2c"
        } -> null
      - tags_all                        = {
          - "Name" = "my-3-tier-architecture-vpc-private-us-west-2c"
        } -> null
      - vpc_id                          = "vpc-0e41b88411b107ccb" -> null
    }

  # module.networking.module.vpc.aws_subnet.public[0] will be destroyed
  - resource "aws_subnet" "public" {
      - arn                             = "arn:aws:ec2:us-west-2:878088820643:subnet/subnet-0b5d9b86e26d2bd6a" -> null
      - assign_ipv6_address_on_creation = false -> null
      - availability_zone               = "us-west-2a" -> null
      - availability_zone_id            = "usw2-az1" -> null
      - cidr_block                      = "10.0.101.0/24" -> null
      - id                              = "subnet-0b5d9b86e26d2bd6a" -> null
      - map_customer_owned_ip_on_launch = false -> null
      - map_public_ip_on_launch         = true -> null
      - owner_id                        = "878088820643" -> null
      - tags                            = {
          - "Name" = "my-3-tier-architecture-vpc-public-us-west-2a"
        } -> null
      - tags_all                        = {
          - "Name" = "my-3-tier-architecture-vpc-public-us-west-2a"
        } -> null
      - vpc_id                          = "vpc-0e41b88411b107ccb" -> null
    }

  # module.networking.module.vpc.aws_subnet.public[1] will be destroyed
  - resource "aws_subnet" "public" {
      - arn                             = "arn:aws:ec2:us-west-2:878088820643:subnet/subnet-0acce62e967c7df6c" -> null
      - assign_ipv6_address_on_creation = false -> null
      - availability_zone               = "us-west-2b" -> null
      - availability_zone_id            = "usw2-az2" -> null
      - cidr_block                      = "10.0.102.0/24" -> null
      - id                              = "subnet-0acce62e967c7df6c" -> null
      - map_customer_owned_ip_on_launch = false -> null
      - map_public_ip_on_launch         = true -> null
      - owner_id                        = "878088820643" -> null
      - tags                            = {
          - "Name" = "my-3-tier-architecture-vpc-public-us-west-2b"
        } -> null
      - tags_all                        = {
          - "Name" = "my-3-tier-architecture-vpc-public-us-west-2b"
        } -> null
      - vpc_id                          = "vpc-0e41b88411b107ccb" -> null
    }

  # module.networking.module.vpc.aws_subnet.public[2] will be destroyed
  - resource "aws_subnet" "public" {
      - arn                             = "arn:aws:ec2:us-west-2:878088820643:subnet/subnet-06ea4d30c5e2bda51" -> null
      - assign_ipv6_address_on_creation = false -> null
      - availability_zone               = "us-west-2c" -> null
      - availability_zone_id            = "usw2-az3" -> null
      - cidr_block                      = "10.0.103.0/24" -> null
      - id                              = "subnet-06ea4d30c5e2bda51" -> null
      - map_customer_owned_ip_on_launch = false -> null
      - map_public_ip_on_launch         = true -> null
      - owner_id                        = "878088820643" -> null
      - tags                            = {
          - "Name" = "my-3-tier-architecture-vpc-public-us-west-2c"
        } -> null
      - tags_all                        = {
          - "Name" = "my-3-tier-architecture-vpc-public-us-west-2c"
        } -> null
      - vpc_id                          = "vpc-0e41b88411b107ccb" -> null
    }

  # module.networking.module.vpc.aws_vpc.this[0] will be destroyed
  - resource "aws_vpc" "this" {
      - arn                              = "arn:aws:ec2:us-west-2:878088820643:vpc/vpc-0e41b88411b107ccb" -> null
      - assign_generated_ipv6_cidr_block = false -> null
      - cidr_block                       = "10.0.0.0/16" -> null
      - default_network_acl_id           = "acl-078cab16017ae2488" -> null
      - default_route_table_id           = "rtb-06ae210a477485e24" -> null
      - default_security_group_id        = "sg-0758be7049f0f9c6e" -> null
      - dhcp_options_id                  = "dopt-4f207137" -> null
      - enable_classiclink               = false -> null
      - enable_classiclink_dns_support   = false -> null
      - enable_dns_hostnames             = false -> null
      - enable_dns_support               = true -> null
      - id                               = "vpc-0e41b88411b107ccb" -> null
      - instance_tenancy                 = "default" -> null
      - main_route_table_id              = "rtb-06ae210a477485e24" -> null
      - owner_id                         = "878088820643" -> null
      - tags                             = {
          - "Name" = "my-3-tier-architecture-vpc"
        } -> null
      - tags_all                         = {
          - "Name" = "my-3-tier-architecture-vpc"
        } -> null
    }

  # module.networking.module.websvr_sg.aws_security_group.security_group will be destroyed
  - resource "aws_security_group" "security_group" {
      - arn                    = "arn:aws:ec2:us-west-2:878088820643:security-group/sg-0f7bb13cfc73fa728" -> null
      - description            = "Managed by Terraform" -> null
      - egress                 = [
          - {
              - cidr_blocks      = [
                  - "0.0.0.0/0",
                ]
              - description      = ""
              - from_port        = 0
              - ipv6_cidr_blocks = []
              - prefix_list_ids  = []
              - protocol         = "-1"
              - security_groups  = []
              - self             = false
              - to_port          = 0
            },
        ] -> null
      - id                     = "sg-0f7bb13cfc73fa728" -> null
      - ingress                = [
          - {
              - cidr_blocks      = [
                  - "10.0.0.0/16",
                ]
              - description      = ""
              - from_port        = 22
              - ipv6_cidr_blocks = []
              - prefix_list_ids  = []
              - protocol         = "tcp"
              - security_groups  = []
              - self             = false
              - to_port          = 22
            },
          - {
              - cidr_blocks      = []
              - description      = ""
              - from_port        = 0
              - ipv6_cidr_blocks = []
              - prefix_list_ids  = []
              - protocol         = "-1"
              - security_groups  = []
              - self             = true
              - to_port          = 0
            },
          - {
              - cidr_blocks      = []
              - description      = ""
              - from_port        = 8080
              - ipv6_cidr_blocks = []
              - prefix_list_ids  = []
              - protocol         = "tcp"
              - security_groups  = [
                  - "sg-0b7b411da05dccc53",
                ]
              - self             = false
              - to_port          = 8080
            },
        ] -> null
      - name                   = "terraform-20211209112459071500000005" -> null
      - name_prefix            = "terraform-" -> null
      - owner_id               = "878088820643" -> null
      - revoke_rules_on_delete = false -> null
      - tags                   = {} -> null
      - tags_all               = {} -> null
      - vpc_id                 = "vpc-0e41b88411b107ccb" -> null
    }

Plan: 0 to add, 0 to change, 40 to destroy.

Changes to Outputs:
  - db_password = (sensitive value)
  - lb_dns_name = "my-3-tier-architecture-220093037.us-west-2.elb.amazonaws.com" -> null

Do you really want to destroy all resources?
  Terraform will destroy all your managed infrastructure, as shown above.
  There is no undo. Only 'yes' will be accepted to confirm.

  Enter a value: yes

module.autoscaling.module.iam_instance_profile.aws_iam_role_policy.iam_role_policy: Destroying... [id=terraform-20211209112432953600000001:terraform-20211209112436676800000002]
module.autoscaling.module.alb.aws_lb_listener.frontend_http_tcp[0]: Destroying... [id=arn:aws:elasticloadbalancing:us-west-2:878088820643:listener/app/my-3-tier-architecture/f7291cfbfbd5d7b8/ca1eb5cce3587811]
module.autoscaling.aws_autoscaling_group.webserver: Destroying... [id=my-3-tier-architecture-asg]
module.autoscaling.module.iam_instance_profile.aws_iam_role_policy.iam_role_policy: Destruction complete after 2s
module.autoscaling.module.alb.aws_lb_listener.frontend_http_tcp[0]: Destruction complete after 2s
module.autoscaling.aws_autoscaling_group.webserver: Still destroying... [id=my-3-tier-architecture-asg, 10s elapsed]
module.autoscaling.aws_autoscaling_group.webserver: Still destroying... [id=my-3-tier-architecture-asg, 20s elapsed]
module.autoscaling.aws_autoscaling_group.webserver: Still destroying... [id=my-3-tier-architecture-asg, 30s elapsed]
module.autoscaling.aws_autoscaling_group.webserver: Still destroying... [id=my-3-tier-architecture-asg, 40s elapsed]
module.autoscaling.aws_autoscaling_group.webserver: Still destroying... [id=my-3-tier-architecture-asg, 50s elapsed]
module.autoscaling.aws_autoscaling_group.webserver: Still destroying... [id=my-3-tier-architecture-asg, 1m0s elapsed]
module.autoscaling.aws_autoscaling_group.webserver: Still destroying... [id=my-3-tier-architecture-asg, 1m10s elapsed]
module.autoscaling.aws_autoscaling_group.webserver: Destruction complete after 1m14s
module.autoscaling.module.alb.aws_lb_target_group.main[0]: Destroying... [id=arn:aws:elasticloadbalancing:us-west-2:878088820643:targetgroup/websvr20211209112919727800000007/1f5b25d1fdcbdece]
module.autoscaling.aws_launch_template.webserver: Destroying... [id=lt-0cc886cecc984456f]
module.autoscaling.module.alb.aws_lb_target_group.main[0]: Destruction complete after 1s
module.autoscaling.module.alb.aws_lb.this[0]: Destroying... [id=arn:aws:elasticloadbalancing:us-west-2:878088820643:loadbalancer/app/my-3-tier-architecture/f7291cfbfbd5d7b8]
module.autoscaling.aws_launch_template.webserver: Destruction complete after 1s
module.autoscaling.module.iam_instance_profile.aws_iam_instance_profile.iam_instance_profile: Destroying... [id=terraform-20211209112436677900000003]
module.database.aws_db_instance.database: Destroying... [id=my-3-tier-architecture-db-instance]
module.autoscaling.module.iam_instance_profile.aws_iam_instance_profile.iam_instance_profile: Destruction complete after 2s
module.autoscaling.module.iam_instance_profile.aws_iam_role.iam_role: Destroying... [id=terraform-20211209112432953600000001]
module.autoscaling.module.alb.aws_lb.this[0]: Destruction complete after 5s
module.autoscaling.module.iam_instance_profile.aws_iam_role.iam_role: Destruction complete after 3s
module.database.aws_db_instance.database: Still destroying... [id=my-3-tier-architecture-db-instance, 10s elapsed]
module.database.aws_db_instance.database: Still destroying... [id=my-3-tier-architecture-db-instance, 20s elapsed]
module.database.aws_db_instance.database: Still destroying... [id=my-3-tier-architecture-db-instance, 30s elapsed]
module.database.aws_db_instance.database: Still destroying... [id=my-3-tier-architecture-db-instance, 40s elapsed]
module.database.aws_db_instance.database: Still destroying... [id=my-3-tier-architecture-db-instance, 50s elapsed]
module.database.aws_db_instance.database: Still destroying... [id=my-3-tier-architecture-db-instance, 1m0s elapsed]
module.database.aws_db_instance.database: Still destroying... [id=my-3-tier-architecture-db-instance, 1m10s elapsed]
module.database.aws_db_instance.database: Still destroying... [id=my-3-tier-architecture-db-instance, 1m20s elapsed]
module.database.aws_db_instance.database: Still destroying... [id=my-3-tier-architecture-db-instance, 1m30s elapsed]
module.database.aws_db_instance.database: Still destroying... [id=my-3-tier-architecture-db-instance, 1m40s elapsed]
module.database.aws_db_instance.database: Still destroying... [id=my-3-tier-architecture-db-instance, 1m50s elapsed]
module.database.aws_db_instance.database: Still destroying... [id=my-3-tier-architecture-db-instance, 2m0s elapsed]
module.database.aws_db_instance.database: Still destroying... [id=my-3-tier-architecture-db-instance, 2m10s elapsed]
module.database.aws_db_instance.database: Still destroying... [id=my-3-tier-architecture-db-instance, 2m20s elapsed]
module.database.aws_db_instance.database: Still destroying... [id=my-3-tier-architecture-db-instance, 2m30s elapsed]
module.database.aws_db_instance.database: Still destroying... [id=my-3-tier-architecture-db-instance, 2m40s elapsed]
module.database.aws_db_instance.database: Still destroying... [id=my-3-tier-architecture-db-instance, 2m50s elapsed]
module.database.aws_db_instance.database: Still destroying... [id=my-3-tier-architecture-db-instance, 3m0s elapsed]
module.database.aws_db_instance.database: Still destroying... [id=my-3-tier-architecture-db-instance, 3m10s elapsed]
module.database.aws_db_instance.database: Still destroying... [id=my-3-tier-architecture-db-instance, 3m20s elapsed]
module.database.aws_db_instance.database: Still destroying... [id=my-3-tier-architecture-db-instance, 3m30s elapsed]
module.database.aws_db_instance.database: Still destroying... [id=my-3-tier-architecture-db-instance, 3m40s elapsed]
module.database.aws_db_instance.database: Still destroying... [id=my-3-tier-architecture-db-instance, 3m50s elapsed]
module.database.aws_db_instance.database: Still destroying... [id=my-3-tier-architecture-db-instance, 4m0s elapsed]
module.database.aws_db_instance.database: Destruction complete after 4m5s
module.networking.module.vpc.aws_route_table_association.public[2]: Destroying... [id=rtbassoc-006e03ba1bfe9ea3e]
module.networking.module.vpc.aws_route.public_internet_gateway[0]: Destroying... [id=r-rtb-0ef7909133d8f121e1080289494]
module.networking.module.vpc.aws_route_table_association.private[0]: Destroying... [id=rtbassoc-093ad37d7dbcc9617]
module.networking.module.vpc.aws_route_table_association.public[0]: Destroying... [id=rtbassoc-0b8ffce252706c0bd]
module.networking.module.vpc.aws_route.private_nat_gateway[0]: Destroying... [id=r-rtb-0441f7cbd2720da871080289494]
module.networking.module.vpc.aws_route_table_association.private[2]: Destroying... [id=rtbassoc-08e06733f874c2dc9]
module.networking.module.vpc.aws_route_table_association.public[1]: Destroying... [id=rtbassoc-0249675b9d2ada026]
module.database.random_password.password: Destroying... [id=none]
module.networking.module.vpc.aws_db_subnet_group.database[0]: Destroying... [id=my-3-tier-architecture-vpc]
module.networking.module.db_sg.aws_security_group.security_group: Destroying... [id=sg-0b119588cc0bd9170]
module.database.random_password.password: Destruction complete after 0s
module.networking.module.vpc.aws_route_table_association.private[1]: Destroying... [id=rtbassoc-09b6e92be25ec25a5]
module.networking.module.vpc.aws_db_subnet_group.database[0]: Destruction complete after 1s
module.networking.module.vpc.aws_route_table_association.database[1]: Destroying... [id=rtbassoc-07d45f374fe2558fa]
module.networking.module.vpc.aws_route_table_association.public[2]: Destruction complete after 2s
module.networking.module.vpc.aws_route_table_association.private[2]: Destruction complete after 2s
module.networking.module.vpc.aws_route_table_association.private[0]: Destruction complete after 2s
module.networking.module.vpc.aws_route_table_association.public[1]: Destruction complete after 2s
module.networking.module.vpc.aws_route_table_association.database[2]: Destroying... [id=rtbassoc-09b002cdbe4859874]
module.networking.module.vpc.aws_route_table_association.database[0]: Destroying... [id=rtbassoc-056cda7f0ab4d0bd2]
module.networking.module.vpc.aws_route_table_association.private[1]: Destruction complete after 2s
module.networking.module.vpc.aws_route_table_association.public[0]: Destruction complete after 2s
module.networking.module.db_sg.aws_security_group.security_group: Destruction complete after 2s
module.networking.module.vpc.aws_subnet.private[1]: Destroying... [id=subnet-098c5b2e22bec80c2]
module.networking.module.vpc.aws_subnet.private[0]: Destroying... [id=subnet-0a21dbdfab358be99]
module.networking.module.vpc.aws_subnet.private[2]: Destroying... [id=subnet-0e0ef959cd3f6ec9a]
module.networking.module.websvr_sg.aws_security_group.security_group: Destroying... [id=sg-0f7bb13cfc73fa728]
module.networking.module.vpc.aws_route.public_internet_gateway[0]: Destruction complete after 3s
module.networking.module.vpc.aws_route_table.public[0]: Destroying... [id=rtb-0ef7909133d8f121e]
module.networking.module.vpc.aws_route.private_nat_gateway[0]: Destruction complete after 3s
module.networking.module.vpc.aws_nat_gateway.this[0]: Destroying... [id=nat-03484b3d7f6c31716]
module.networking.module.vpc.aws_route_table_association.database[1]: Destruction complete after 2s
module.networking.module.vpc.aws_route_table_association.database[2]: Destruction complete after 2s
module.networking.module.vpc.aws_route_table_association.database[0]: Destruction complete after 2s
module.networking.module.vpc.aws_subnet.database[1]: Destroying... [id=subnet-0fa28647c54f6cb2b]
module.networking.module.vpc.aws_subnet.database[0]: Destroying... [id=subnet-04315cb26c7deb411]
module.networking.module.vpc.aws_subnet.database[2]: Destroying... [id=subnet-0925364cf17643020]
module.networking.module.vpc.aws_route_table.private[0]: Destroying... [id=rtb-0441f7cbd2720da87]
module.networking.module.vpc.aws_subnet.private[1]: Destruction complete after 3s
module.networking.module.vpc.aws_subnet.private[0]: Destruction complete after 3s
module.networking.module.vpc.aws_subnet.private[2]: Destruction complete after 3s
module.networking.module.websvr_sg.aws_security_group.security_group: Destruction complete after 3s
module.networking.module.lb_sg.aws_security_group.security_group: Destroying... [id=sg-0b7b411da05dccc53]
module.networking.module.vpc.aws_route_table.public[0]: Destruction complete after 4s
module.networking.module.vpc.aws_subnet.database[2]: Destruction complete after 3s
module.networking.module.vpc.aws_subnet.database[1]: Destruction complete after 3s
module.networking.module.vpc.aws_subnet.database[0]: Destruction complete after 3s
module.networking.module.lb_sg.aws_security_group.security_group: Destruction complete after 3s
module.networking.module.vpc.aws_route_table.private[0]: Destruction complete after 4s
module.networking.module.vpc.aws_nat_gateway.this[0]: Still destroying... [id=nat-03484b3d7f6c31716, 10s elapsed]
module.networking.module.vpc.aws_nat_gateway.this[0]: Still destroying... [id=nat-03484b3d7f6c31716, 20s elapsed]
module.networking.module.vpc.aws_nat_gateway.this[0]: Still destroying... [id=nat-03484b3d7f6c31716, 30s elapsed]
module.networking.module.vpc.aws_nat_gateway.this[0]: Still destroying... [id=nat-03484b3d7f6c31716, 40s elapsed]
module.networking.module.vpc.aws_nat_gateway.this[0]: Still destroying... [id=nat-03484b3d7f6c31716, 50s elapsed]
module.networking.module.vpc.aws_nat_gateway.this[0]: Destruction complete after 57s
module.networking.module.vpc.aws_internet_gateway.this[0]: Destroying... [id=igw-0ef2ef5261f219c4a]
module.networking.module.vpc.aws_subnet.public[1]: Destroying... [id=subnet-0acce62e967c7df6c]
module.networking.module.vpc.aws_subnet.public[2]: Destroying... [id=subnet-06ea4d30c5e2bda51]
module.networking.module.vpc.aws_subnet.public[0]: Destroying... [id=subnet-0b5d9b86e26d2bd6a]
module.networking.module.vpc.aws_eip.nat[0]: Destroying... [id=eipalloc-0c271d80e0b96839c]
module.networking.module.vpc.aws_subnet.public[0]: Destruction complete after 3s
module.networking.module.vpc.aws_subnet.public[1]: Destruction complete after 3s
module.networking.module.vpc.aws_subnet.public[2]: Destruction complete after 3s
module.networking.module.vpc.aws_eip.nat[0]: Destruction complete after 3s
module.networking.module.vpc.aws_internet_gateway.this[0]: Still destroying... [id=igw-0ef2ef5261f219c4a, 10s elapsed]
module.networking.module.vpc.aws_internet_gateway.this[0]: Destruction complete after 12s
module.networking.module.vpc.aws_vpc.this[0]: Destroying... [id=vpc-0e41b88411b107ccb]
module.networking.module.vpc.aws_vpc.this[0]: Destruction complete after 1s

Destroy complete! Resources: 40 destroyed.
