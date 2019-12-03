# AWS Route53 Terraform Module 

A Terraform module which allows creating and managing AWS Route53 zones.

This type of resource is supported :
- [ROUTE53 - aws_route53_zone](https://www.terraform.io/docs/providers/aws/r/route53_zone.html)

# Features

The goal of this module is to give a standard way of creatingcand managing Route53 public and private Zones.
The module supports :

* For public Zone
    - Name
    - Comments
    - Tags

* For public SubZone
    - Name
    - Zone ID
    - Comments
    - Tags

* For private Zone
    - Name
    - VPC ID
    - Comments
    - Tags

## Terraform versions

Support of Terraform 0.12 is not yet implemented. (WIP)

If you are using Terraform 0.11 you can use versions `v1.*`.

## Usage

Public Zone creation example: 

```hcl
module "aws_route53_public" {
  source           = "app.terraform.io/<ORG_NAME>/route53/aws"
  pubic_zone_name = ["demoaws.my-v-world.com"]
  comment          = ["Used internally for HashiCorp Demos"]
}
```

Public SubZone creation example: 

```hcl
data "aws_route53_zone" "zone" {
    name = "my-v-world.com"
}

module "aws_route53_public" {
  source           = "app.terraform.io/<ORG_NAME>/route53/aws"
  public_zone_name = ["demoaws.my-v-world.com"]
  zone_id           =  "${data.aws_route53_zone.zone.zone_id}"
  comment          = ["Used internally for HashiCorp Demos"]
}
```

Private Zone creation example: 

```hcl
data "aws_vpc" "vpc"{
    name = "vpc1"
}

module "aws_route53_public" {
  source           = "app.terraform.io/<ORG_NAME>/route53/aws"
  private_zone_name = ["internal.my-v-world.com","test.my-v-world.com"]
  vpc_id           =  "${data.aws_vpc.vpc.vpc_id}"
  comment          = ["Used internally for HashiCorp Demos", "Used for testing"]
}
```

## Authors

* **Nicolas Ehrman** - *Initial work* - [Hashicorp](https://www.hashicorp.com)



