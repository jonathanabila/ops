FROM python:3.8.5-slim

ENV KUBECTL_URL="https://storage.googleapis.com/kubernetes-release/release"
ENV DEBIAN_FRONTEND="noninteractive"

# Installing some basics
RUN apt-get update \
    && apt-get install -y \
        curl git unzip gcc \
        python-dev libffi-dev libc-dev \
        apt-transport-https ca-certificates gnupg-agent software-properties-common apt-utils \
    && apt-get purge -y --auto-remove \
    && rm -rf /var/lib/apt/lists/*

# Installing Terraform
RUN curl -LO https://releases.hashicorp.com/terraform/0.14.3/terraform_0.14.3_linux_amd64.zip
RUN unzip terraform_0.14.3_linux_amd64.zip
RUN rm -rf terraform_0.14.3_linux_amd64.zip
RUN mv terraform /usr/bin

# Installing AWS CLI
RUN pip3 install awscli

# Installing Kubctl
RUN curl -LO "${KUBECTL_URL}/$(curl -s ${KUBECTL_URL}/stable.txt)/bin/linux/amd64/kubectl"
RUN chmod +x ./kubectl && mv ./kubectl /usr/local/bin/kubectl

RUN curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add -
RUN add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/debian $(lsb_release -cs) stable"
RUN apt-get update \
    && apt-get install -y docker-ce

# Installing Docker Compose
RUN curl -L "https://github.com/docker/compose/releases/download/1.27.4/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
RUN chmod +x /usr/local/bin/docker-compose
