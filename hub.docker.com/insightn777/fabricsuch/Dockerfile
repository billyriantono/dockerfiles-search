##########################################
# Dockerfile
# Hyperledger/fabric
# eetue/such
##########################################

# 1. Base Image    // docker가 bionic(Ubuntu 18.04.1 LTS) 까지만 지원
FROM ubuntu:18.04 AS fabricbase
# set ARG    // ARG must be after FROM
ARG name=value
# dependencies installqq
RUN apt-get update && apt-get install -y apt-utils \
    && apt-get install -y curl python-pip git libltdl-dev tree openssh-server net-tools vim apt-transport-https software-properties-common
# go install & mkdir
RUN curl -sL https://dl.google.com/go/go1.10.4.linux-amd64.tar.gz | tar -C /usr/local -zx && mkdir -p /root/eetue/gopath /root/eetue/myfabric
# go env    // 이상하게 PATH는 따로 ENV 안주면 적용안됨
ENV GOPATH=/root/eetue/gopath \
    GOROOT=/usr/local/go
ENV PATH=$PATH:$GOROOT/bin
# docker install
RUN curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add - \
    && add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" \
    && apt-get update && apt-get install -y docker-ce && pip install docker-compose
# fabric core/ca install
RUN mkdir -p $GOPATH/src/github.com/hyperledger && cd $GOPATH/src/github.com/hyperledger \ 
    && git clone -b release-1.4 https://github.com/hyperledger/fabric && git clone -b release-1.4 https://github.com/hyperledger/fabric-ca
    WORKDIR /root/eetue/myfabric

# ----------------------------------------
# 2. CA Image
FROM fabricbase AS ca
# ca-client / server install
RUN mkdir /root/eetue/myfabric/ca-server /root/eetue/myfabric/ca-admin /root/eetue/myfabric/org-admin && cd $GOPATH/src/github.com/hyperledger/fabric-ca && make fabric-ca-server && make fabric-ca-client
ENV PATH=$PATH:$GOPATH/src/github.com/hyperledger/fabric-ca/bin \
    FABRIC_CA_SERVER_HOME=/root/eetue/myfabric/ca-server \
    FABRIC_CA_CLIENT_HOME=/root/eetue/myfabric/org-admin
EXPOSE 7054
# ----------------------------------------
# 3. orderer Image
FROM fabricbase AS orderer
# ca-client install
RUN cd $GOPATH/src/github.com/hyperledger/fabric-ca && make fabric-ca-client
ENV PATH=$PATH:$GOPATH/src/github.com/hyperledger/fabric-ca/bin
# orderer install     // FABRIC_CFG_PATH 에는 core.yaml 이 있어야됨
RUN cd $GOPATH/src/github.com/hyperledger/fabric && make configtxgen && make orderer
ENV FABRIC_HOME=$GOPATH/src/github.com/hyperledger/fabric \
    PATH=$PATH:$GOPATH/src/github.com/hyperledger/fabric/.build/bin \
    FABRIC_CFG_PATH=/root/eetue/myfabric \
    FABRIC_CA_CLIENT_HOME=/root/eetue/myfabric
RUN cd $FABRIC_HOME/sampleconfig && cp core.yaml $FABRIC_CFG_PATH && cp orderer.yaml $FABRIC_CFG_PATH # cd는 RUN마다 해줘야됨
EXPOSE 7050
# ----------------------------------------
# 4. Peer Image
FROM fabricbase AS peer
# ca-client install
RUN cd $GOPATH/src/github.com/hyperledger/fabric-ca && make fabric-ca-client
ENV PATH=$PATH:$GOPATH/src/github.com/hyperledger/fabric-ca/bin
# peer install     // FABRIC_CFG_PATH 에는 core.yaml 이 있어야됨
RUN cd $GOPATH/src/github.com/hyperledger/fabric && make peer
ENV FABRIC_HOME=$GOPATH/src/github.com/hyperledger/fabric \
    PATH=$PATH:$GOPATH/src/github.com/hyperledger/fabric/.build/bin \
    FABRIC_CFG_PATH=/root/eetue/myfabric \
    FABRIC_CA_CLIENT_HOME=/root/eetue/myfabric
RUN cd $FABRIC_HOME/sampleconfig && cp core.yaml $FABRIC_CFG_PATH && cp orderer.yaml $FABRIC_CFG_PATH
EXPOSE 7051 7053
# ----------------------------------------
###########################################################################################
