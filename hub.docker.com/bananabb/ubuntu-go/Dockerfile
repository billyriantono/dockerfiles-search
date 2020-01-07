FROM bananabb/ubuntu-base:base.3.0.0
MAINTAINER BananaBb

# Install Go
RUN sudo apt-get update -y \
 && mkdir -p /var/src \
 && curl -O https://dl.google.com/go/go1.11.linux-amd64.tar.gz \
 && tar -xvf go1.11.linux-amd64.tar.gz \
 && mv go /usr/local \
 && rm go1.11.linux-amd64.tar.gz

# Set ENV
ENV GOROOT /usr/local/go
ENV GOPATH $HOME/go
ENV PATH $GOPATH/bin:$GOROOT/bin:$PATH

# Create working Directory
WORKDIR /var/src
EXPOSE 80 443

CMD ["/bin/bash"]