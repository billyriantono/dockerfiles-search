FROM lvlds/docker-android-sdk

RUN mkdir /app/ && \
    apt-get update && \
    apt-get install -y curl git && \
    curl -sL https://deb.nodesource.com/setup_5.x | bash - && \
    apt-get install -y nodejs
RUN npm install -g ionic@beta 
RUN npm install -g cordova 
RUN npm install -g gulp
RUN npm install -g bower

ENTRYPOINT ["bash"]
