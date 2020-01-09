FROM codercom/code-server:1.1156-vsc1.33.1

USER root
RUN sudo apt-get update \
&&  sudo apt-get install -y apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common \
    lsb-release \
    software-properties-common \
&&  curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add - \
&&  sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" \
&&  sudo apt-get update \
&&  sudo apt-get install -y docker-ce=5:18.09.7~3-0~ubuntu-bionic 