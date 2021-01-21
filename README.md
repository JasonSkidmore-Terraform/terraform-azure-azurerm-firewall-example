# terraform-azurerm-firewall-example

## How to use

Login to Azure account. I am using my personal free Azure account for testing and demoing

`az login`


1. To view the current Azure subscription, use [az account show]()https://docs.microsoft.com/en-us/cli/azure/account#az-account-show.

    `az account show`

2. If you have access to multiple available Azure subscriptions, use [az account list](https://docs.microsoft.com/en-us/cli/azure/account#az-account-list) to display a list of subscription name ID values:

    `az account list --query "[].{name:name, subscriptionId:id}"`

3. To use a specific Azure subscription for the current Cloud Shell session, use [az account set](https://docs.microsoft.com/en-us/cli/azure/account#az-account-set). Replace the <subscription_id> placeholder with the ID (or name) of the subscription you want to use:

Notes:

Calling `az account set` doesn't display the results of switching to the specified Azure subscription. However, you can use `az account show` to confirm that the current Azure subscription has changed.

### Create and apply a Terraform execution plan

1. To initialize the Terraform deployment, run terraform init. This command downloads the Azure modules required to create an Azure resource group.

    `terraform init`

2. After initialization, you create an execution plan by running terraform plan.

    `terraform plan -out <terraform_plan>.tfplan`


Notes:

* The terraform plan command creates an execution plan, but doesn't execute it. Instead, it determines what actions are necessary to create the configuration specified in your configuration files. This pattern allows you to verify whether the execution plan matches your expectations before making any changes to actual resources.
* The optional -out parameter allows you to specify an output file for the plan. Using the -out parameter ensures that the plan you reviewed is exactly what is applied.
* To read more about persisting execution plans and security, see the [security warning section](https://www.terraform.io/docs/commands/plan.html#security-warning).

3. Once you're ready to apply the execution plan to your cloud infrastructure, you run terraform apply.

    `terraform apply <terraform_plan>.tfplan`

### Reverse a Terraform execution plan

1. To reverse, or undo, the execution plan, you run terraform plan and specify the destroy flag as follows:

    `terraform plan -destroy -out <terraform_plan>.destroy.tfplan`

2. Run terraform apply to apply the execution plan.
   
   `terraform apply <terraform_plan>.destroy.tfplan`


