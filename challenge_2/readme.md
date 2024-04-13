# Challenge 2 - A introduction to IaC and Terraform

## Assumed knowledge

* Basic linux

## What is Infrastructure as Code (IaC)

Infrastructure as Code (IaC) tools allow you to manage infrastructure with configuration files rather than through a graphical user interface. IaC allows you to build, change, and manage your infrastructure in a safe, consistent, and repeatable way by defining resource configurations that you can version, reuse, and share. [terraform.io](https://developer.hashicorp.com/terraform/tutorials/aws-get-started/infrastructure-as-code)


*Creating a virtual machine* [ref](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/linux_virtual_machine)
```hcl
resource "azurerm_linux_virtual_machine" "example" {
  name                = "example-machine"
  resource_group_name = azurerm_resource_group.example.name
  location            = azurerm_resource_group.example.location
  size                = "Standard_F2"
  admin_username      = "adminuser"

  network_interface_ids = [
    azurerm_network_interface.example.id,
  ]

  admin_ssh_key {
    username   = "adminuser"
    public_key = file("~/.ssh/id_rsa.pub")
  }

  os_disk {
    caching              = "ReadWrite"
    storage_account_type = "Standard_LRS"
  }

  source_image_reference {
    publisher = "Canonical"
    offer     = "0001-com-ubuntu-server-jammy"
    sku       = "22_04-lts"
    version   = "latest"
  }
}
```


## Deploying infrastructure with Terraform

You have to use the terraform cli to deploy the infrastructure. The terraform cli is a command line tool that allows you to interact with terraform configurations.

```sh
terraform init
terraform plan
terraform apply # This will deploy the infrastructure
```

```sh
terraform destroy # This will destroy the infrastructure
```

## Challenge 🔈

Create a terraform configuration that deploys a virtual machine in Azure.

Tip: navigate to the `./example` directory. The terraform code is already there, you need to figure out how to deploy it. 

Usefull links:
* [Terraform](https://www.terraform.io/)
* [Installing Azure CLI](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli)
* [Authenticating terraform to azure](https://learn.microsoft.com/en-us/azure/developer/terraform/authenticate-to-azure?tabs=bash)
