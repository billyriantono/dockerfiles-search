FROM  ubuntu:trusty
ENV PATH $PATH:/home/vivansa/dart/bin
RUN apt update && apt upgrade -y && apt install -y wget unzip git ssh tar gzip ca-certificates
RUN mkdir /app && chmod 777 /app
RUN useradd vivansa -m -d /home/vivansa \
 && chown -R vivansa /app 
USER vivansa
WORKDIR /home/vivansa
RUN wget https://storage.googleapis.com/dart-archive/channels/stable/release/1.15.0/sdk/dartsdk-linux-x64-release.zip \
  && unzip dartsdk-linux-x64-release.zip \
  && mv dart-sdk dart \
  && rm -rf dartsdk-linux-x64-release.zip \
  && chmod go+rx /home/vivansa/dart




