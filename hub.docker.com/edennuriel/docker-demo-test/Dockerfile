from mysql

RUN apt-get update
RUN apt-get install -y curl lsb-release

## Installing gcloud for deb / ubuntu
RUN export CLOUD_SDK_REPO="cloud-sdk-$(lsb_release -c -s)" && echo "deb http://packages.cloud.google.com/apt $CLOUD_SDK_REPO main" | tee -a /etc/apt/sources.list.d/google-cloud-sdk.list
RUN ls -l /etc/apt/sources.list.d
RUN cat /etc/apt/sources.list.d/google-cloud-sdk.list
RUN curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add -
RUN apt-get update && apt-get install -y google-cloud-sdk


RUN mkdir -p /backup/data
RUN mkdir -p /app

ADD run /backup/run
WORKDIR /backup

ENTRYPOINT ["./run"]
CMD ['backup']
