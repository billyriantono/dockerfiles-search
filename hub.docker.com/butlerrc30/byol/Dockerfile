FROM mcr.microsoft.com/powershell
RUN pwsh -c 'Set-PSRepository -Name "PSGallery" -InstallationPolicy Trusted' && \
apt-get update && \
apt-get install wget unzip python software-properties-common python-pip jq -y && \
pip install awscli --upgrade && \
pwsh -c 'install-module VMware.PowerCLI -force -confirm:$false' && \
pwsh -c 'Set-PowerCLIConfiguration -InvalidCertificateAction:Ignore -confirm:$false' && \
wget https://releases.hashicorp.com/packer/1.4.0/packer_1.4.0_linux_amd64.zip && \
unzip packer_1.4.0_linux_amd64.zip -d /usr/bin && \
wget https://github.com/jetbrains-infra/packer-builder-vsphere/releases/download/v2.3/packer-builder-vsphere-iso.linux -P /usr/bin && \
chmod +x /usr/bin/packer-builder-vsphere-iso.linux && \
apt-add-repository ppa:ansible/ansible && \
apt-get update && \
apt-get install ansible -y