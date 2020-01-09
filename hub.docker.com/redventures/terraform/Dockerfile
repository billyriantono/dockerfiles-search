FROM debian

run mkdir -v /opt/terraform

RUN apt-get update && apt-get install -y curl unzip git make python3.4 python-setuptools python-dev build-essential 
RUN easy_install pip 
RUN pip install --upgrade --user awscli

# install terraform
RUN cd /tmp && curl https://releases.hashicorp.com/terraform/0.9.5/terraform_0.9.5_linux_amd64.zip -L -o tf.zip && \
  unzip tf.zip && \
  rm -rf tf.zip && \
  mv terraform /usr/bin/terraform9 && \
  chmod 555 /usr/bin/terraform9 && \
  ln -s /usr/bin/terraform9 /usr/bin/terraform

WORKDIR /opt/terraform

CMD ["/bin/bash"]
