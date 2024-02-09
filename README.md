# DevOps GitHub Actions Terraform AWS
![example workflow](https://github.com/github/docs/actions/workflows/main.yml/badge.svg)

Automate and manage your infrastructure on AWS with GitHub Actions and Terraform! This repository provides ready-to-use workflows that integrate powerful automation tools, allowing you to provision and manage resources in the cloud efficiently.

## Resources

- Designed to accelerate development and continuous delivery (CI/CD).
- Easy and ready-to-use configuration with Terraform and AWS.
- Customizable workflows to meet your specific DevOps needs.
- Teaches best practices for applying and removing resources with Terraform, including detailed steps for apply and destroy.
- Utilizes a Terraform provider to connect to AWS and manage resources in the cloud.

## How to Use

1. Fork this repository.
2. Clone the fork to your local environment.
3. Configure necessary environment variables in GitHub.
4. Customize the workflows as needed for your project.

## Provider Configuration

The first step when working with Terraform is configuring the provider, which is responsible for communicating with the cloud provider (in our case, AWS) and performing operations on resources. To do this, we use the provider block in Terraform code.

In Terraform, the provider is a fundamental part that establishes the connection with a cloud provider such as AWS, Azure, Google Cloud, among others. To enable Terraform to interact with the cloud infrastructure, it's necessary to correctly configure the provider, which includes providing access credentials.

Access credentials are required to authenticate to the cloud and perform operations on resources. In the specific case of AWS, access credentials typically consist of an Access Key ID and a Secret Access Key.

These credentials can be configured in various ways, including using local configuration files, environment variables, or in cloud environments, by associating an IAM Role with the instance where Terraform is being executed.

Here's an example:

```hcl
provider "aws" {
  region = "us-east-1"
}
```
In the example below, we can see how AWS access credentials are configured as environment variables in a GitHub Actions workflow:

```yaml
jobs:
  meu_job:
    runs-on: ubuntu-latest
    env:
      TF_VERSION: "1.0.11"
      AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
      AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}

```

## Workflow

This workflow performs the following steps:

1. **Checkout code:** Checks out the code from the repository.
2. **Setup Terraform:** Sets up Terraform with the specified version.
3. **Configure AWS credentials:** Configures AWS access credentials using GitHub Secrets.
4. **Terraform init:** Initializes Terraform in the working directory.
5. **Terraform plan:** Generates an execution plan for Terraform.
6. **Terraform apply:** Applies the Terraform execution plan, automatically approving any changes.

In this workflow, the AWS access key ID and secret access key are stored as secrets in the GitHub repository settings, providing a secure way to access AWS resources within the workflow.



## Terraform State

The Terraform state - the terraform.tfstate file - is a record of provisioned resources and their current configuration, enabling Terraform to understand and manage changes to the infrastructure accurately. It tracks information such as resource IDs, metadata, and dependencies between resources. This state is crucial for Terraform to determine what needs to be modified, created, or removed in each execution, ensuring consistency between the declarative description in the Terraform code and the actual state of the infrastructure in the cloud. Terraform state can be stored locally or in remote storage to facilitate teamwork and ensure the security of sensitive information.

The terraform.tfstate file contains sensitive information, and its exposure can pose serious security risks. This file includes details about the provisioned infrastructure, including resource IDs, IP addresses, and access keys. If exposed, an attacker can use this information to compromise the security of the infrastructure.

Furthermore, the state file may contain authentication credentials such as API keys and access tokens, which if accessed by unauthorized third parties, can be exploited to gain unauthorized access to the infrastructure.

To protect the Terraform state file, it's essential to store it securely, limit access only to authorized team members, and avoid accidental exposure. It's recommended to use cloud storage services with appropriate access controls or secure secret management solutions like HashiCorp's Vault.

In summary, securing the Terraform state file is critical to ensuring the security of cloud infrastructure and preventing potential security breaches.


## Contributing

Feel free to contribute with improvements, bug fixes, or new features! Just open an issue or submit a pull request.

## License

This project is licensed under [MIT License](LICENSE).
