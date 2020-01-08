FROM ubuntu:18.04
LABEL maintener: YukiMiyatake<YukiMariaMiyatake@gmail.com>

WORKDIR /root
ENV HOME /root

#apt
RUN apt-get update && apt-get install -y curl unzip wget python python3-pip software-properties-common

#ngrok
RUN curl -O https://bin.equinox.io/c/4VmDzA7iaHb/ngrok-stable-linux-amd64.zip \
    && unzip ngrok-stable-linux-amd64.zip
ENV PATH=$HOME/ngrok/bin:$PATH

#dotnet core
RUN wget -q https://packages.microsoft.com/config/ubuntu/18.04/packages-microsoft-prod.deb -O packages-microsoft-prod.deb \
    && dpkg -i packages-microsoft-prod.deb \
    && add-apt-repository universe \
    && apt-get install -y apt-transport-https \
    && apt-get update \
    && apt-get install -y dotnet-sdk-2.2

#node
RUN apt-get install -y perl \
    && curl -L git.io/nodebrew | perl - setup
ENV PATH=$HOME/.nodebrew/current/bin:$PATH 
RUN ls -al $HOME/.nodebrew/current/bin

RUN nodebrew install v8.10 \
    && nodebrew install v10.15 \
    && nodebrew use v10.15 
RUN npm config set user 0 \
    && npm config set unsafe-perm true
RUN npm update -g

#AWS-cli
#RUN curl "https://bootstrap.pypa.io/get-pip.py" -o "get-pip.py" \
#    python get-pip.py \
#    pip install awscli
RUN pip3 install awscli

#azure-cli
RUN curl -sL https://aka.ms/InstallAzureCLIDeb | bash

#GCP

#Alibaba
RUN pip3 install -U aliyun-log-cli 

RUN apt-get install -y libsecret-1-dev
#serverless framework
RUN npm install -g -y serverless 
RUN npm install -g serverless-azure-functions

WORKDIR /src

#serverless create --template azure-nodejs --path my-service --name my-unique-name
#dotnet resutore  dotnet build
#CMD [ngrok http -host-header="0.0.0.0:7071" 7071]


