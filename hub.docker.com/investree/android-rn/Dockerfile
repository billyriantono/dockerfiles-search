FROM investree/android:latest

MAINTAINER Feri Setiyawan <feri.setiyawan@investree.id>

ENV NODE_VERSION 8.11.3
RUN cd && \
    wget -q http://nodejs.org/dist/v${NODE_VERSION}/node-v${NODE_VERSION}-linux-x64.tar.gz && \
    tar -xzf node-v${NODE_VERSION}-linux-x64.tar.gz && \
    mv node-v${NODE_VERSION}-linux-x64 /opt/node && \
    rm node-v${NODE_VERSION}-linux-x64.tar.gz
ENV PATH ${PATH}:/opt/node/bin

RUN npm install react-native-cli -g
RUN npm install yarn -g

