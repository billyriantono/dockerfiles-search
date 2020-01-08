FROM centos:7
ENV SDK_NAME google-cloud-sdk-223.0.0-linux-x86_64.tar.gz
ADD https://dl.google.com/dl/cloudsdk/channels/rapid/downloads/$SDK_NAME .
RUN tar zxvf $SDK_NAME google-cloud-sdk
ENV PATH $PWD/google-cloud-sdk/bin:$PATH
