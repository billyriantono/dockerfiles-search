FROM node:12.9.0
RUN apt-get update && \
    npm i -g ionic cordova && \
    npm i -g firebase-tools && \
    npm i -g cordova-res --unsafe-perm=true --allow-root && \
    # npm i -g gem && \
    #apt-get install ruby -y && \
    #apt-get install rubygems -y && \
    apt-get install ruby-dev -y && \
    gem install fastlane -NV