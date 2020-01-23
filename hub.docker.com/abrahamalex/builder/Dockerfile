FROM ubuntu:xenial
RUN adduser --disabled-password --gecos '' circleci
ENV CLOUDSDK_CORE_DISABLE_PROMPTS 1
ENV PATH /opt/google-cloud-sdk/bin:$PATH
RUN apt-get update -y
RUN apt-get install -y jq \
      libapparmor-dev \
      libseccomp-dev \
      gettext \
      build-essential\
      python-dev \
      python-pip
RUN pip install protobuf
RUN pip install pyyaml
RUN pip install commentjson
RUN curl https://sdk.cloud.google.com | bash && mv /root/google-cloud-sdk /opt
RUN gcloud components install kubectl
RUN pip install awscli
RUN gcloud components install docker-credential-gcr
RUN gcloud components install beta
RUN curl -L https://github.com/docker/compose/releases/download/1.19.0/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
RUN chmod +x /usr/local/bin/docker-compose
RUN gcloud components install docker-credential-gcr
COPY install-bazel.sh /
COPY sam_0.2.8_linux_amd64.deb /
RUN apt update && apt install -y gdebi && gdebi -n /sam_0.2.8_linux_amd64.deb
RUN . /install-bazel.sh
RUN apt-get install -y build-essential
RUN apt-get install -y python3 python3-pip
RUN pip3 install awscli
RUN apt-get install -y git
USER circleci
CMD ["bazel"]
