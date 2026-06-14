#Dockerfile for runner image

# Use an official, stable lightweight base image
FROM ubuntu:22.04

# Prevent interactive prompts during installation
ENV DEBIAN_FRONTEND=noninteractive

# Install core system dependencies
RUN apt-get update && apt-get install -y --no-install-recommends \
    curl \
    unzip \
    ca-certificates \
    gnupg \
    git \
    python3 \
    python3-pip \
    && rm -rf /var/lib/apt/lists/*

# Fix python symlinks
RUN ln -s /usr/bin/python3 /usr/bin/python

# 1. INSTALL TERRAFORM (Pin your exact version here)
ARG TERRAFORM_VERSION=1.6.2
RUN curl -sSL https://releases.hashicorp.com/terraform/${TERRAFORM_VERSION}/terraform_${TERRAFORM_VERSION}_linux_amd64.zip -o terraform.zip \
    && unzip terraform.zip \
    && mv terraform /usr/local/bin/ \
    && rm terraform.zip

# 2. INSTALL TFLINT
RUN curl -s https://raw.githubusercontent.com/terraform-linters/tflint/master/install_linux.sh | bash

# 3. INSTALL TFSEC
RUN curl -s https://raw.githubusercontent.com/aquasecurity/tfsec/master/scripts/install_linux.sh | bash

# 4. INSTALL CHECOKV VIA PIP
RUN pip install --no-cache-dir checkov

# Verify installations when building
RUN terraform --version \
    && tflint --version \
    && tfsec --version \
    && checkov --version

# Set default execution environment
CMD ["/bin/bash"]


# Steps to use this docker file for runner

#@@@@@ Step 1. Build and Version the Image Locally
# # Build the image locally and tag it as v1.0.0
# docker build -t corpcregistry.azurecr.io/devops/tf-runner:1.0.0 .

#@@@@@ Step 2 : Push the Image to Your Private Registry

# Authenticate to your registry
# az acr login --name corpcregistry

# Push the image to the cloud repository
# docker push corpcregistry.azurecr.io/devops/tf-runner:1.0.0

#@@@@@ Step 3 : Update Your Variable Configuration
# variables:
#    - name: CONTAINER_RUNNER
#      value: 'corpcregistry.azurecr.io/devops/tf-runner:1.0.0'



# on AWS :
# Authenticate to AWS ECR
# aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 123456789012.dkr.ecr.us-east-1.amazonaws.com

# Tag and push
# docker tag corpcregistry.azurecr.io/devops/tf-runner:1.0.0 123456789012.dkr.ecr.us-east-1.amazonaws.com/devops/tf-runner:1.0.0
# docker push 123456789012.dkr.ecr.us-east-1.amazonaws.com/devops/tf-runner:1.0.0

