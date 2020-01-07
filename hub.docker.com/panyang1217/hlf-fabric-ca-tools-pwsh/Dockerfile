FROM hyperledger/fabric-ca-tools:latest
RUN apt-get update
RUN apt-get install apt-transport-https -y
RUN curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
RUN curl -o /etc/apt/sources.list.d/microsoft.list https://packages.microsoft.com/config/ubuntu/16.04/prod.list 
RUN apt-get update 
RUN apt-get install -y powershell