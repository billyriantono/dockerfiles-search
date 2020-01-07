FROM library/ubuntu

#Install SFDX CLI
RUN apt-get update && \
    apt-get -y install wget && \
    apt-get -y install xz-utils && \
    cd ~ && \
    wget https://developer.salesforce.com/media/salesforce-cli/sfdx-linux-amd64.tar.xz -O sfdx.tar.xz && \
    tar -xJf ~/sfdx.tar.xz && \
    cd sfdx* && \
    ./install;
    

RUN sfdx update;
    
#Install jq
RUN apt-get install -y jq;