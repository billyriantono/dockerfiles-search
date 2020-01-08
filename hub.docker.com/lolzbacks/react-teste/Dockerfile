FROM ubuntu

RUN apt-get update
RUN sed -i -e 's/us.archive.ubuntu.com/archive.ubuntu.com/g' /etc/apt/sources.list && \
    apt-get update && \
    apt-get install -y curl

RUN apt-get update
RUN curl -sL https://deb.nodesource.com/setup_10.x |  bash \
  && apt-get install -y nodejs
RUN npm install -g npm@6.4.1

RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - && \
  echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list
RUN apt update && \ 
  apt install yarn 
  
RUN yarn global add react-devtools
RUN yarn add global node-sass 

RUN npm install -g react-native-cli
RUN apt install -y openjdk-8-jdk openjdk-8-jre

ENV ADB_IP="192.168.112.101"
ENV REACT_NATIVE_PACKAGER_HOSTNAME="192.168.1.1"
RUN apt install -y adb
RUN apt install wget
RUN mkdir ~/android

RUN wget https://dl.google.com/android/repository/sdk-tools-linux-4333796.zip
RUN apt install unzip
RUN unzip -d ~/android/sdk sdk-tools-linux-4333796.zip
RUN echo 'export ANDROID_HOME=$HOME/android/sdk' >> ~/.bashrc
RUN echo 'export PATH=$PATH:$ANDROID_HOME/tools:$ANDROID_HOME/tools/bin' >> ~/.bashrc

RUN apt install -y git
RUN apt-get update && \
    apt-get install usbutils

#Ao dar run na imagem, executar "docker run -ti -d --privileged -v /dev/bus/usb:/dev/bus/usb nome_da_imagem" com o dispositivo conectado
# e depois dar exec no container que foi iniciado

#Ao entrar no container, rodar o seguinte comando para aceitar os termos  ~/android/sdk/tools/bin/./sdkmanager "add-ons;addon-google_apis-google-24" "build-tools;28.0.3" "platforms;android-28"
