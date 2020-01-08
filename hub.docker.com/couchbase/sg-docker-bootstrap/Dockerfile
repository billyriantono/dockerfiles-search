FROM centos:centos7

ENV GOPATH /opt/go
ENV GOROOT /usr/local/go
ENV PATH $PATH:$GOPATH/bin:$GOROOT/bin

# Get dependencies
RUN yum -y update && \
    yum install -y \
    bc \
    curl \
    git \
    wget 

# Download and install Go
RUN wget http://golang.org/dl/go1.7.3.linux-amd64.tar.gz && \
    tar -C /usr/local -xzf go1.7.3.linux-amd64.tar.gz && \
    rm go1.7.3.linux-amd64.tar.gz

# Download repo tool
RUN curl https://storage.googleapis.com/google-code-archive-downloads/v2/code.google.com/git-repo/repo-1.19 -o repo && \
    chmod +x repo

# Git config to avoid repo errors when running bootstrap.sh 
RUN git config --global user.email "build@couchbase.com" && \
    git config --global user.name "Couchbase Build"

# Download bootstrap.sh script 
RUN wget https://raw.githubusercontent.com/couchbase/sync_gateway/master/bootstrap.sh && \
    chmod +x bootstrap.sh
