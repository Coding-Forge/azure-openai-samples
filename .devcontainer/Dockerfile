FROM mcr.microsoft.com/vscode/devcontainers/miniconda:latest

ARG USER=vscode
ARG openai_rg_name=${resource_group}
ARG openai_svc_name=${azure_openai_instance}
ARG subscription=${subscription_id}
ARG OPENAI_API_KEY=${OPENAI_API_KEY}
ARG OPENAI_API_BASE=${OPENAI_API_BASE}
ARG azure_openai_instance=${azure_openai_instance}

ENV openai_rg_name $openai_rg_name
ENV openai_svc_name $openai_svc_name
ENV subscription $subscription
ENV OPEANAI_API_KEY = $OPENAI_API_KEY
ENV OPEANAI_API_BASE = $OPENAI_API_BASE
ENV azure_openai_instance = $azure_openai_instance
ENV SETUSER $USER

WORKDIR /home/$SETUSER

# Create the environment:
COPY environment.yml .
RUN conda env create -f environment.yml

RUN echo ". /opt/conda/etc/profile.d/conda.sh" >> ~/.bashrc && \
    echo "conda activate base" >> ~/.bashrc

RUN	sudo apt-get update && sudo apt-get -y install curl
RUN	sudo apt-get update -y

# Azure installation command
RUN	curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash
# az extension add -n ml -y

SHELL ["conda", "run", "-n", "oai", "/bin/bash", "-c"]