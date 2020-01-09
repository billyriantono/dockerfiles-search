FROM whitaker/ubuntu
MAINTAINER Jason Whitaker <jason@thewhitakers.ca>

RUN apt-get update && \
    add-apt-repository ppa:webupd8team/java && \
    apt-get update
RUN echo debconf shared/accepted-oracle-license-v1-1 select true | debconf-set-selections 
RUN echo debconf shared/accepted-oracle-license-v1-1 seen true | debconf-set-selections  
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y oracle-java8-installer oracle-java8-set-default

