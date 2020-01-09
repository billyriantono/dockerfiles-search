#Dockerfile used for auto build https://hub.docker.com/r/robertjensen/cas
FROM ubuntu:latest
WORKDIR /tmp
#Update imnage and install essesntial apps
RUN apt-get update && apt-get install -y \
    curl \
    python \
    sshpass \
    wget \
    unzip \
    git \
    jq \
    nano \
    && rm -rf /var/lib/apt/lists/* && \
    #Install packer
    wget https://releases.hashicorp.com/packer/1.3.5/packer_1.3.5_linux_amd64.zip && \
    unzip *.zip && \
    rm packer_1.3.5_linux_amd64.zip && \
    mv packer /usr/sbin && \
    #Install Powershell
    wget -q https://packages.microsoft.com/config/ubuntu/18.04/packages-microsoft-prod.deb && \
    dpkg -i packages-microsoft-prod.deb && \
    apt update -y && \
    apt install powershell -y && \
    #Cleanup image tmp dir
    rm -rf /tmp/*
    # Install VMware modules from PSGallery
SHELL [ "pwsh", "-command" ]
RUN Set-PSRepository -Name PSGallery -InstallationPolicy Trusted
RUN Install-Module VMware.PowerCLI,PowerNSX,PowervRA
RUN Set-PowerCLIConfiguration -InvalidCertificateAction:ignore -Confirm:$false
CMD ["/bin/pwsh"]



