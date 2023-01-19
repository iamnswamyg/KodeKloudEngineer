### 1. What is Terraform?
Terraform is one of the most popular IAC tools used by every cloud engineer. It allows us to define both cloud and on-premise resources in human-readable configuration files and thereby provision these resources programmatically. The most notable feature of Terraform is that, unlike most IAC tools out there, it is not limited to a single cloud provider. You can use Terraform to run your applications on multiple cloud platforms simultaneously.

### 2. What do you understand by Terraform?
Terraform is an open-source IAC tool created by HashiCorp. It is used to create, update, delete and version your infrastructure on multiple cloud platforms.

### 3. What are the reasons to choose Terraform for DevOps?
Using Terraform for provisioning infrastructure leaves no room for human errors, hence improving the quality, consistency, and efficiency of Cloud and on-prem infrastructure. Terraform uses the HCL language, which is fairly similar to JSON and easy to learn and use. Unlike the other IAC tools offered by cloud providers like Cloudformation for AWS, we can use Terraform with a number of cloud platforms simultaneously. This avoids the need to learn multiple IAC tools and improves the scope of collaboration.

### 4. Why is Terraform used for DevOps?
Terraform uses a JSON-like configuration language called the HashiCorp Configuration Language (HCL). HCL has a very simple syntax that makes it easy for DevOps teams to define and enforce infrastructure configurations across multiple clouds and on-premises data centers.

### 5. What are the key features of Terraform?
Terraform helps you manage all of your infrastructures as code and construct it as and when needed. Here are its key main features:
- A console that allows users to observe functions 
- The ability to translate HCL code into JSON format
- A configuration language that supports interpolation 
- A module count that keeps track of the number of modules applied to the infrastructure.

### 6. Define IAC?
IAC or Infrastructure as Code allows you to build, change, and manage your infrastructure through coding instead of manual processes. The configuration files are created according to your infrastructure specifications and these configurations can be edited and distributed securely within an organization.

### 7. What do you mean by Terraform cloud?
Terraform Cloud is a remote environment that is optimized for the Terraform workflow. It provides features like workspaces and state locking, which allows people in big teams to collaborate.

### 8. How does Terraform work?
Terraform uses plugins called the Terraform providers to interact with APIs on Cloud Platforms and provision our resources. As an end-user, terraform workflow has three steps.
- Write: Author the infrastructure as code.
- Plan: Preview changes Terraform will make before applying.
- Apply: Provision the infrastructure and apply the changes.

### 9. What are the most useful Terraform commands?
Some of the most useful Terraform commands are:
- terraform init - initializes the current directory
- terraform refresh - refreshes the state file
- terraform output - views Terraform outputs
- terraform apply - applies the Terraform code and builds stuff
- terraform destroy - destroys what has been built by Terraform
- terraform graph - creates a DOT-formatted graph
- terraform plan - a dry run to see what Terraform will do

### 10. What is Terraform init?
Terraform init is a control to initialize an operational index that contains Terraform pattern files. This control can be looped multiple times. It is the first command that should be run after writing the new Terraform design.

### 11. What do you understand by State in Terraform?
As an IAC tool, terraform should know the current state of configurations and infrastructure under its management. Terraform stores this information in a file called the state file.

### 12. What is a provider in Terraform?
Providers in Terraform are plugins that allow Terraform to interact with cloud providers, SaaS providers, and other APIs. For example, if we plan on using Terraform to provision infrastructure on AWS, we will need to declare an AWS provider in our configuration files.

### 13. Who maintains Terraform Providers?
Providers are distributed separately from Terraform itself. As a Terraform user, anyone can develop their own providers. There are some standard providers that are maintained explicitly by Hashicorp.

### 14. Define null resource in Terraform.
null_resource implements standard resource library, but no further action is taken.

### 15. What do you understand by Terraform Backend?
Terraform backend is the platform where the Terraform State Snapshots are stored. By default, Terraform uses a backend called local to store state as a local file on your disk. All other supported backends are some kind of remote storage service.

### 16. Explain the uses of Terraform CLI and list some basic CLI commands?
The Terraform Command-Line Interface (CLI) is used to manage infrastructure and interact with Terraform state, configuration files, providers, etc.
Here are some basic CLI commands:
- terraform init - prepares your working directory for other commands
- terraform destroy - destroys the previously-created infrastructure
- terraform validate - check whether the configuration is valid
- terraform apply - creates or updates the infrastructure
- terraform plan - shows changes needed by the current configuration

### 17. What are modules in Terraform?
A jug for numerous resources that are used jointly is known as a module in Terraform. The root module includes resources mentioned in the .tf files and is required for every Terraform.

### 18. Is Terraform usable for an on-prem infrastructure?
Yes, Terraform can be used for on-prem infrastructure. As there are a lot of obtainable providers, we can decide which suits us the best. All that we need is an API

### 19. Does Terraform support multi-provider deployments?
Yes, multi-provider deployments are supported by Terraform, which includes on-prem like Openstack, VMware.

### 20. How is duplicate resource error ignored during terraform apply?
We can try the following options:
- Delete those resources from the cloud provider(API) and recreate them using Terraform
- Delete those resources from Terraform code to stop its management with it
- Carry out a terraform import of the resource and remove the code that is trying to recreate them

### 21. What are Provisioners in Terraform?
Provisioners are Terraform resources used to execute scripts as a part of the resource creation or destruction. There are two types of Provisioners in Terraform:
- local-exec: Invokes a script on the machine running Terraform.
- remote- exec: Invokes a script on a remote resource after it is created.
Provisioners are only meant to be used as a last resort in Terraform.

### 22. What is the external data block in Terraform?
Just like the local-exec provisioner, external data bock can be used to run scripts on machines running Terraform. The difference between a provisioner and the external data block is that the scripts in the external data block can return data in JSON format, whereas provisioners cannot return any outputs. It is important to note that external data blocks are also meant to be a last resort and should not be used if there is a better alternative.

### 23. How can two people using the Terraform cloud can create two different sets of infrastructure using the same working directory?
By using different workspaces. These users can start Terraform runs in two separate workspaces. Each workspace has a state file of its own, so as long as the resources do not overlap, both the users can successfully provision two different sets of infrastructure using the same code.

### 24. What happens when multiple engineers start deploying infrastructure using the same state file?
Terraform has a very important feature called “state locking”. This feature ensures that no changes are made to the state file during a run and prevents the state file from getting corrupt. It is important to note that not all Terraform Backends support the state locking feature. You should choose the right backend if this feature is a requirement.

### 25. How can you use the same provider in Terraform with different configurations?
By using alias argument in the provider block.
```
provider "aws" {
  alias = "default"
  region = "us-west-2"
}

provider "aws" {
  alias = "secondary"
  region = "us-east-1"
}

resource "aws_s3_bucket" "bucket1" {
  provider = "aws.default"
  bucket = "example-bucket-1"
}

resource "aws_s3_bucket" "bucket2" {
  provider = "aws.secondary"
  bucket = "example-bucket-2"
}
```

### 26. You have a Terraform configuration file with no resources. What happens when you run the terraform apply command?
Terraform will destroy all the resources. Starting an empty run with terraform apply command is exactly the same as starting the terraform destroy run.

### 27. What happens if a resource was created successfully in terraform but failed during provisioning?
This is an unlikely scenario, but when this happens, the resource is marked as tainted and can be recreated by restarting the terraform run.

### 28. Which value of the TF_LOG variable provides the MOST verbose logging?
TRACE is the most verbose and the default value of the TF_LOG variable.

### 29. How can you import existing resources under Terraform Management?
By using the terraform import command.
Let's say you have an existing S3 bucket called "example-bucket" in your AWS account and you want to manage it with Terraform.
```
terraform import aws_s3_bucket.example example-bucket
```
This command tells Terraform to import the S3 bucket resource named "example-bucket" and assign it to the aws_s3_bucket.example resource block in your Terraform configuration. Once you've run the import command, Terraform will update its state to reflect the current state of the imported resource. You can then make changes to the resource block in your configuration and use the terraform apply command to update the resource.

### 30. Which command can be used to preview the terraform execution plan?
The terraform plan command generates the execution plan of the changes Terraform will do to the infrastructure.

### 31. Which command can be used to reconcile the Terraform state with the actual real-world infrastructure?
The terraform apply -refresh-only command is used to reconcile Terraform state with the actual real-world infrastructure. It is the new alternative to the terraform refresh command, which is now deprecated.

### 32. Which command is used to perform syntax validation on terraform configuration files?
The terraform validate command is used to verify whether a configuration is syntactically valid and internally consistent.

### 33. Which command is used to create new workspaces in the Terraform cloud?
- The **terraform workspace new <workspace-name>** command is used to create a new workspace.
The **terraform workspace select <workspace-name>** command is used to choose a different workspace.

### 34. Which command destroys Terraform managed infrastructure?
The given command is used for this purpose:
```
terraform destroy [options] [dir]
```

### 35. Tell us about some notable Terraform applications.
The applications of Terraform are pretty broad due to its facility of extending its abilities for resource manipulation. Some of the unique applications are:
- Software demos development
- Resource schedulers
- Multi-cloud deployment
- Disposable environment creations
- Multi-tier applications development
- Self-service clusters
- Setup of Heroku App

### 36. What are the components of Terraform architecture?
The Terraform architecture includes the following features:
- Sub-graphs
- Expression Evaluation
- Vertex Evaluation
- Graph Walk
- Graph Builder
- State Manager
- Configuration Loader
- CLI (Command Line interface)
- Backend

### 37. Define Resource Graph in Terraform.
A resource graph is a visual representation of the resources. It helps modify and create independent resources simultaneously. Terraform establishes a plan for the configuration of the graph to generate plans and refresh the state. It creates structure most efficiently and effectively to help us understand the drawbacks.

### 38. What is Sentinel?
Sentinel is a policy as a code tool used to enforce standard configurations for resources being deployed by Terraform. It can be used by organizations for compliance and governance purposes.
```
# policy.sentinel
import "tfplan"

# Define the naming convention for S3 buckets
bucket_name_regex = "^example-[a-z]+$"

# Check if the name of the S3 bucket matches the naming convention
# and raise an error if it doesn't
main = rule {
  all tfplan.resources.aws_s3_bucket as _, r {
    r.applied.bucket =~ bucket_name_regex
  }
}

# main.tf
resource "aws_s3_bucket" "example" {
  bucket = "example-bucket"
}
```
In this example, the Sentinel policy is defined in a separate file called policy.sentinel. The policy imports the tfplan module and defines a regular expression for the naming convention of S3 buckets. The main rule then checks if the name of the aws_s3_bucket resource matches the naming convention and raises an error if it doesn't.

To use the Sentinel policy, you would run the Terraform command with the -var-file option to specify the path to the Sentinel policy file.
```
$ terraform plan -var-file=policy.sentinel
```
This way any time you run terraform plan, it will check for the sentinel policy before applying any change.

### 39. Can you provide a few examples where we can use for Sentinel policies?
Sentinels are a powerful way to implement a variety of policies in Terraform. Here are a few examples:
- Enforce explicit ownership in resources
- Restrict roles the cloud provider can assume
- Review an audit trail for Terraform Cloud operations
- Forbid only certain resources, providers, or data sources
- Enforce mandatory tagging on resources 
- Restrict how modules are used in the Private Module Registry

### 40. What are the various levels of Sentinel enforcement?
Sentinel has three enforcement levels - advisory, soft mandatory, and hard mandatory.
- Advisory - Logged but allowed to pass. An advisory is issued to the user when they trigger a plan that violates the policy.
- Soft Mandatory - The policy must pass unless an override is specified. Only administrators have the ability to override.
- Hard Mandatory - The policy must pass no matter what. This policy cannot be overridden unless it is removed. It is the default enforcement level in Terraform.

### 41. What do you understand by modules in Terraform?
A Terraform module is a standard container for multiple resources used together to provision and configure resources. For example, you can create a “VPC module” for your organization that provisions a standard VPC and other resources like Subnets and Internet Gateways. Modules can be shared publically via the Public module registry and privately via the Private Module registry.

### 42. What is the benefit of using modules in terraform?
Terraform modules allow us to create logical abstraction on the top of a resource set. Using modules allows us to maintain and reuse a standard configuration for resources. They can be versioned and shared with members of your teams to provision resources in a standard way.

### 43. What is the Private Module Registry?
A Private Module Registry Terraform Cloud feature allows us to share Terraform modules across our organization.

### 44. How to Store Sensitive Data in Terraform?
Terraform requires credentials to communicate with your cloud provider's API. But most of the time, these credentials are saved in plaintext on your desktop. GitHub is exposed to thousands of API and cryptographic keys every day. Hence, your API keys should never be stored in Terraform code directly.  You should use encrypted storage to store all your passwords, TLS certificates, SSH keys, and anything else that shouldn't be stored in plain text.

### 45. Explain State File Locking?
State file locking is Terraform mechanism in which operations on a specific state file are blocked to avoid conflicts between multiple users performing the same process. When one user releases the lock, then only the other one can operate on that state. This helps in preventing state file corruption. This is a backend operation.

### 46. What do you understand by a Tainted Resource?
A tainted resource is a resource that is forced to be destroyed and recreated on the next apply command. When a resource is marked as tainted, the state files are updated, but nothing changes on infrastructure. The terraform plan out shows that resource will get destroyed and recreated. The changes get implemented when the next apply happens.

### 47. How to lock Terraform module versions?
A proven way of locking Terraform module version is using the Terraform module registry as a source. We can use the ‘version’ attribute in module of the Terraform configuration file.
``` 
module "example" {
  source = "module-registry.example.com/my-module"
  version = "1.2.3"
}
```
### 48. What is Terraform Core? Tell us some primary responsibilities of it.
Terraform Core is a binary written statically compiled by using the Go programming language. The compiled binary offers an entry point for the users of Terraform. The primary responsibilities include:
- Reading and interpolation of modules and configuration files by Infrastructure as code functionalities
- Resource Graph Construction
- Plugin communication through RPC
- Plan execution
- Management of resource state

### 49. Give the terraform configuration for creating a single EC2 instance on AWS.
This is the Terraform configuration for creating a single EC2 instance on AWS:
```
provider “aws” {
region = “”
}
resource “aws_instance” “example” {
ami = ""
instance_type = ""
tags {
 Name = "example"
}
}
```

### 50. How will you upgrade plugins on Terraform?
Run ‘terraform init’ with ‘-upgrade’ option. This command rechecks the releases.hashicorp.com to find new acceptable provider versions. It also downloads available provider versions. “.terraform/plugins/<OS>_<ARCH>” is the automatic downloads directory.

### 51. How can we export data from one module to another?
We can export data from a module by defining output blocks in the module configuration files. This data can then be transferred as a parameter to the destination module.

### 52. How will you make an object of one module available for the other module at a high level?
```
# lower-level module
output "example_object" {
  value = var.example_object
}

# higher-level module
module "lower_level_module" {
  source = "path/to/lower-level-module"
  example_object = var.example_object
}

variable "example_object" {}

resource "example_resource" {
  example_object = module.lower_level_module.example_object
}
```
In this example, the example_object variable in the higher-level module references the output of the same name in the lower-level module, and is then passed as input to the example_resource.

### 53. How can you define dependencies in Terraform?
Terraform has built-in dependency management. Terraform has two kinds of dependencies between resources- implicit and explicit dependencies.
- Implicit dependencies, as the name suggests, are detected by Terraform automatically. This is when the output of a “resource A” is used in “resource B”. Terraform automatically detects that “resource B” needs to be created only after “resource A”
- Explicit dependencies can be specified in cases where two resources are internally dependent on each other without sharing any outputs. This can be done by using the depends_on parameter in the configuration block.

### 54. How will you control and handle rollbacks when something goes wrong?
I need to recommit the previous code version to be the new and current version in my VCS. This would trigger as terraform run, which would be responsible for running the old code. As Terraform is more declarative, I will make sure all things in the code roll back to the old code. I would use the State Rollback Feature of Terraform Enterprise to roll back to the latest state if the state file got corrupted.

### 55. What is DataSource?
Data sources allow Terraform to use information defined outside of Terraform, defined by another separate Terraform configuration, or modified by functions. A data source is accessed via a special kind of resource known as a data resource, declared using a data block.
```
data "aws_ami" "example" {
  most_recent = true

  owners = ["self"]
  tags = {
    Name   = "app-server"
    Tested = "true"
  }
}
```