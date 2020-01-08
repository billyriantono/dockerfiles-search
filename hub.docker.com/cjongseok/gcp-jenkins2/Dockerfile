FROM launcher.gcr.io/google/jenkins2@sha256:9d1233c1779f7ac464515aa91fbf631f6d1c7b832a6328e73213e9f4662e720b

ENV CLOUDSDK_CORE_DISABLE_PROMPTS 1
ENV PATH /opt/google-cloud-sdk/bin:/usr/local/bin:$PATH
ENV PYTHON_VER 2.7.14
ENV PYTHONPATH /usr/local/lib/python2.7/site-packages

USER root

RUN apt-get update -y
RUN apt-get install -y jq \
      libapparmor-dev \
      libseccomp-dev \
      build-essential \
      zlib1g-dev \
      libssl-dev \
      libsqlite3-dev
RUN curl -L https://www.python.org/ftp/python/${PYTHON_VER}/Python-${PYTHON_VER}.tgz > /opt/Python-${PYTHON_VER}.tgz && cd /opt && tar xzf Python-${PYTHON_VER}.tgz
RUN cd /opt/Python-${PYTHON_VER} && ./configure && make && make install
RUN curl https://sdk.cloud.google.com | bash && mv /root/google-cloud-sdk /opt/
RUN gcloud components install kubectl
USER jenkins
