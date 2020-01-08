FROM ubuntu:18.04

RUN apt-get update && \
    apt-get install -y apt-transport-https ca-certificates curl software-properties-common && \
    (curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add -) && \
    (curl -sL https://deb.nodesource.com/setup_8.x | bash -) && \
    (curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -) && \
    (echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list) && \
    (add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable")

ENV NODEJS_VERSION 8.10.0~dfsg-2ubuntu0.4

RUN apt-get update -y && \
    apt-get install -y python3-pip groff nodejs=${NODEJS_VERSION} yarn git \
                       jq docker-ce nodejs yarn curl build-essential gnupg zip \
                       unzip wget vim
RUN pip3 install awscli --upgrade && \
    pip3 install --upgrade setuptools

# https://askubuntu.com/questions/1036278/npm-is-incorrect-version-on-latest-ubuntu-18-04-installation
RUN npm install -g npm && \
    apt-get purge npm -y && \
    ln -fs /usr/local/bin/npm /bin/npm

ENV TERRAFORM_VERSION 0.11.13

RUN mkdir /tmp/terraform && \
    curl https://releases.hashicorp.com/terraform/${TERRAFORM_VERSION}/terraform_${TERRAFORM_VERSION}_linux_amd64.zip -o /tmp/terraform/terraform.zip && \
    cd /tmp/terraform && \
    unzip terraform.zip && \
    mv terraform /bin/terraform && \
    chmod +x /bin/terraform && \
    rm -rf /tmp/terraform

ENV TERRAGRUNT_VERSION 0.18.2

RUN curl -sL https://github.com/gruntwork-io/terragrunt/releases/download/v${TERRAGRUNT_VERSION}/terragrunt_linux_amd64 -o /bin/terragrunt && \
    chmod +x /bin/terragrunt

ENV PATH=$PATH:/root/bin

RUN yarn global add gatsby-cli

COPY ./scripts/ss-aws-account-profile-add.sh /usr/local/bin/ss-aws-account-profile-add
COPY ./scripts/ss-aws-role-profile-add.sh /usr/local/bin/ss-aws-role-profile-add

RUN rm -rf /var/lib/apt/lists/* && apt-get clean && apt-get autoclean && apt-get autoremove -y

WORKDIR /code
