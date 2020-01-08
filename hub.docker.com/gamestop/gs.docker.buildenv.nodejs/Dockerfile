FROM ubuntu:16.04

ENV VERSION="node_10.x"
ENV DISTRO="xenial"

RUN apt-get -y update && apt-get upgrade -y && \
    apt-get install -y software-properties-common \
                       wget \
                       apt-transport-https \
                       git 

# using manual install instructions from https://github.com/nodesource/distributions/blob/master/README.md#debmanual 
# which maintains the official node packages for ubunto package managers
RUN add-apt-repository -y -r ppa:chris-lea/node.js && \
    rm -f /etc/apt/sources.list.d/chris-lea-node_js-*.list && \
    rm -f /etc/apt/sources.list.d/chris-lea-node_js-*.list.save

RUN wget --quiet -O - https://deb.nodesource.com/gpgkey/nodesource.gpg.key | apt-key add -



RUN echo "deb https://deb.nodesource.com/$VERSION $DISTRO main" | tee /etc/apt/sources.list.d/nodesource.list && \
    echo "deb-src https://deb.nodesource.com/$VERSION $DISTRO main" | tee -a /etc/apt/sources.list.d/nodesource.list

RUN apt-get update && \
    apt-get install -y nodejs

RUN npm install --global yarn@1.3.2

CMD [ "node" ]