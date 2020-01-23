FROM beevelop/android-nodejs:v6.11.1

# use bash instead of sh
RUN rm /bin/sh && ln -s /bin/bash /bin/sh

RUN apt-get update -y --fix-missing && \
    apt-get install -y git && \
    apt-get install -y build-essential&& \
    apt-get install -y libssl-dev && \
    apt-get install -y python python-dev python-distribute python-pip && \
    apt-get install -y ruby && \
    apt-get install -y sshpass

RUN npm config set registry https://registry.npm.taobao.org && \
    npm install -g react-native-cli && \
    npm install -g supervisor && \
    npm install -g bower && \
    npm install -g webpack && \
    npm install -g pm2 && \
    npm install -g bunyan

# Clean up
RUN rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* && \
    apt-get autoremove -y && \
    apt-get clean
