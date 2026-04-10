<!-- BEGIN_TF_DOCS -->
## Requirements

| Name | Version |
|------|---------|
| <a name="requirement_terraform"></a> [terraform](#requirement\_terraform) | >= 1.10.0 |
| <a name="requirement_azurerm"></a> [azurerm](#requirement\_azurerm) | >= 4.0 |

## Providers

| Name | Version |
|------|---------|
| <a name="provider_azurerm"></a> [azurerm](#provider\_azurerm) | >= 4.0 |

## Modules

| Name | Source | Version |
|------|--------|---------|
| <a name="module_nat_gateway"></a> [nat\_gateway](#module\_nat\_gateway) | ./modules/nat_gateway | n/a |
| <a name="module_route_table"></a> [route\_table](#module\_route\_table) | ./modules/route_table | n/a |

## Resources

| Name | Type |
|------|------|
| [azurerm_subnet.subnet](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/subnet) | resource |
| [azurerm_subnet_nat_gateway_association.subnet_assoc](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/subnet_nat_gateway_association) | resource |
| [azurerm_subnet_network_security_group_association.nsg_subnet_association](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/subnet_network_security_group_association) | resource |
| [azurerm_subnet_route_table_association.main](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/subnet_route_table_association) | resource |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| <a name="input_deployment_mode"></a> [deployment\_mode](#input\_deployment\_mode) | Specifies how the infrastructure/resource is deployed | `string` | `"terraform"` | no |
| <a name="input_enable"></a> [enable](#input\_enable) | Flag to control the module creation. | `bool` | `true` | no |
| <a name="input_enable_nat_gateway"></a> [enable\_nat\_gateway](#input\_enable\_nat\_gateway) | Flag to control nat gateway creation. | `bool` | `false` | no |
| <a name="input_enable_route_table"></a> [enable\_route\_table](#input\_enable\_route\_table) | Flag to control route table creation. | `bool` | `false` | no |
| <a name="input_environment"></a> [environment](#input\_environment) | Environment (e.g. `prod`, `dev`, `staging`). | `string` | `null` | no |
| <a name="input_extra_tags"></a> [extra\_tags](#input\_extra\_tags) | Variable to pass extra tags. | `map(string)` | `null` | no |
| <a name="input_label_order"></a> [label\_order](#input\_label\_order) | The order of labels used to construct resource names or tags. If not specified, defaults to ['name', 'environment', 'location']. | `list(string)` | <pre>[<br/>  "name",<br/>  "environment",<br/>  "location"<br/>]</pre> | no |
| <a name="input_location"></a> [location](#input\_location) | The location/region where the virtual network is created. | `string` | `""` | no |
| <a name="input_managedby"></a> [managedby](#input\_managedby) | ManagedBy, eg 'terraform-az-modules'. | `string` | `"terraform-az-modules"` | no |
| <a name="input_nat_gateways"></a> [nat\_gateways](#input\_nat\_gateways) | List of NAT Gateways to create | <pre>list(object({<br/>    name                     = string<br/>    sku_name                 = optional(string, "Standard")<br/>    nat_gateway_idle_timeout = optional(number, 4)<br/>    zones                    = optional(list(string), [])<br/>  }))</pre> | `[]` | no |
| <a name="input_repository"></a> [repository](#input\_repository) | Terraform current module repo | `string` | `"https://github.com/terraform-az-modules/terraform-azure-subnet.git"` | no |
| <a name="input_resource_group_name"></a> [resource\_group\_name](#input\_resource\_group\_name) | The name of an existing resource group to be imported. | `string` | `null` | no |
| <a name="input_route_tables"></a> [route\_tables](#input\_route\_tables) | List of route tables with their configuration. | <pre>list(object({<br/>    name                          = string<br/>    bgp_route_propagation_enabled = optional(bool, false)<br/>    routes = optional(list(object({<br/>      name                   = string<br/>      address_prefix         = string<br/>      next_hop_type          = string<br/>      next_hop_in_ip_address = optional(string)<br/>    })), [])<br/>  }))</pre> | `[]` | no |
| <a name="input_subnets"></a> [subnets](#input\_subnets) | List of subnets to create | <pre>list(object({<br/>    name                          = string<br/>    subnet_prefixes               = list(string)<br/>    nat_gateway_name              = optional(string)<br/>    route_table_name              = optional(string)<br/>    nsg_association               = optional(bool, false)<br/>    service_endpoints             = optional(list(string), [])<br/>    service_endpoint_policy_ids   = optional(list(string), [])<br/>    private_link_service_policies = optional(bool, true)<br/>    private_endpoint_policies     = optional(string, "Enabled")<br/>    default_outbound_access       = optional(bool, true)<br/>    network_security_group_id     = optional(string, null)<br/>    delegations = optional(list(object({<br/>      name = string<br/>      service_delegations = list(object({<br/>        name    = string<br/>        actions = list(string)<br/>      }))<br/>    })), [])<br/>  }))</pre> | `[]` | no |
| <a name="input_virtual_network_name"></a> [virtual\_network\_name](#input\_virtual\_network\_name) | Name of the virtual network | `string` | `null` | no |

## Outputs

| Name | Description |
|------|-------------|
| <a name="output_nat_gateway_ids"></a> [nat\_gateway\_ids](#output\_nat\_gateway\_ids) | Map of NAT Gateway names to their IDs. |
| <a name="output_nat_gateway_names"></a> [nat\_gateway\_names](#output\_nat\_gateway\_names) | Map of NAT Gateway names to their names. |
| <a name="output_public_ip_addresses"></a> [public\_ip\_addresses](#output\_public\_ip\_addresses) | Map of NAT Gateway names to their associated public IP addresses. |
| <a name="output_public_ip_ids"></a> [public\_ip\_ids](#output\_public\_ip\_ids) | Map of NAT Gateway names to their associated public IP resource IDs. |
| <a name="output_route_table_ids"></a> [route\_table\_ids](#output\_route\_table\_ids) | Map of route table names to their IDs. |
| <a name="output_route_table_names"></a> [route\_table\_names](#output\_route\_table\_names) | Map of route table names to their names. |
| <a name="output_subnet_address_prefixes"></a> [subnet\_address\_prefixes](#output\_subnet\_address\_prefixes) | Map of subnet names to their address prefixes. |
| <a name="output_subnet_ids"></a> [subnet\_ids](#output\_subnet\_ids) | Map of subnet names to their IDs. |
| <a name="output_subnet_names"></a> [subnet\_names](#output\_subnet\_names) | Map of subnet names to their names. |
<!-- END_TF_DOCS -->