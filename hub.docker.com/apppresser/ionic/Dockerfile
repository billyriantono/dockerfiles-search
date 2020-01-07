FROM node:10

ENV IONIC_VERSION 5.4.2

RUN apt-get update && apt-get install -y git bzip2 openssh-client && \
    npm i -g --unsafe-perm ionic@${IONIC_VERSION} && \
    ionic --no-interactive config set -g daemon.updates false && \
    npm install @ionic-native/core @ionic-native/action-sheet @ionic-native/admob-free @ionic-native/camera @ionic-native/device @ionic-native/dialogs @ionic-native/facebook @ionic-native/file @ionic-native/file-transfer @ionic-native/geolocation @ionic-native/in-app-browser @ionic-native/in-app-purchase @ionic-native/keyboard @ionic-native/network @ionic-native/push @ionic-native/social-sharing @ionic-native/splash-screen @ionic-native/status-bar @ionic-native/streaming-media @ionic-native/transfer && \ 
    npm install @ionic/storage @ngx-translate/core @ngx-translate/http-loader anchorme && \
    rm -rf /var/lib/apt/lists/* && apt-get clean
