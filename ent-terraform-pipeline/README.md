# Introduction 
TODO: Give a short introduction of your project. Let this section explain the objectives or the motivation behind this project. 

# Getting Started
TODO: Guide users through getting your code up and running on their own system. In this section you can talk about:
1.	Installation process
2.	Software dependencies
3.	Latest releases
4.	API references

# Build and Test
TODO: Describe and show how to build your code and run the tests. 

# Contribute
TODO: Explain how other users and developers can contribute to make your code better. 

If you want to learn more about creating good readme files then refer the following [guidelines](https://docs.microsoft.com/en-us/azure/devops/repos/git/create-a-readme?view=azure-devops). You can also seek inspiration from the below readme files:
- [ASP.NET Core](https://github.com/aspnet/Home)
- [Visual Studio Code](https://github.com/Microsoft/vscode)
- [Chakra Core](https://github.com/Microsoft/ChakraCore)


# Step 1: Setting up the Pipeline Repository (pipeline-templates)

pipeline-templates/
├── .gitignore
├── README.md
└── src/
    ├── jobs/
    │   ├── tf-pr-validation-job.yml
    │   └── tf-deploy-job.yml
    └── steps/
        ├── tf-fmt-validate-lint.yml
        ├── tf-init.yml
        ├── tf-security-scan.yml
        ├── tf-plan.yml
        └── tf-apply.yml



# Step 2: Setting up the Terraform Application Repository (tf-infrastructure-app)

tf-infrastructure-app/
├── .gitignore
├── README.md
├── .pipelines/
│   ├── pr-pipeline.yml
│   └── deploy-pipeline.yml
├── modules/
│   ├── networking/
│   └── compute/
└── src/
    ├── main.tf
    ├── variables.tf
    ├── outputs.tf
    ├── providers.tf
    └── environments/
        ├── dev/
        │   ├── dev.tfvars
        │   └── backend.conf
        └── prod/
            ├── prod.tfvars
            └── backend.conf