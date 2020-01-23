FROM quay.io/openshiftio/che-ubuntu_jdk8
RUN sudo apt-get update && sudo apt-get install apt-transport-https lsb-release software-properties-common dirmngr wget -y
RUN AZ_REPO=$(lsb_release -cs) && echo "deb [arch=amd64] https://packages.microsoft.com/repos/azure-cli/ $AZ_REPO main" | sudo tee /etc/apt/sources.list.d/azure-cli.list
RUN sudo apt-key --keyring /etc/apt/trusted.gpg.d/Microsoft.gpg adv --keyserver packages.microsoft.com --recv-keys BC528686B50D79E339D3721CEB3E94ADBE1229CF
RUN wget -q https://packages.microsoft.com/config/ubuntu/16.04/packages-microsoft-prod.deb
RUN sudo dpkg -i packages-microsoft-prod.deb
RUN sudo apt-get update && sudo apt-get install azure-cli && sudo npm install -g azure-functions-core-tools
RUN sudo apt-get install dotnet-sdk-2.2 -y
  
