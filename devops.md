m
vpc.tf

```
provider "aws"{
	region = "ap-south-1"
}

//create vpc
//subnets 
//create internet gateway
//create route table association
//create security groups
//create ec2
```

resources:
aws_vpc
3 aws_subnet - 1a,1b,1c(change vpc id) add map_public_ip_on_launch = true
aws_internet_gateway
aws_route_table (cidr range to 0.0.0.0/0 for public access)
3 aws_route_table_association
aws_security_group
aws_instance