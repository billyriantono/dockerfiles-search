# werckerビルド環境: Java8+Google Cloud SDK
FROM tsccloud/wercker-jdk:8
MAINTAINER Technosite Cloud
RUN apt-get -y update; \
    apt-get -y upgrade; \
    apt-get -y install \
        lsb-release; \
    export CLOUD_SDK_REPO="cloud-sdk-$(lsb_release -c -s)"; \
    echo "deb http://packages.cloud.google.com/apt $CLOUD_SDK_REPO main" | sudo tee -a /etc/apt/sources.list.d/google-cloud-sdk.list; \
    curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -; \
    apt-get -y update; \
    apt-get -y install google-cloud-sdk; \
    apt-get -y install google-cloud-sdk-app-engine-java; \
    apt-get clean; \
    apt-get autoclean; \
    apt-get autoremove
