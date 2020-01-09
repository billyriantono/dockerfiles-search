FROM alpine:3

RUN apk add --update ca-certificates \
        git \
        openssh-client \
        openssl \
        python3\
        rsync \
        sshpass \
        unzip \
        bash \
        ansible
RUN apk del .build-deps || true \
        && rm -rf /var/cache/apk/*
WORKDIR /root

# install packer
RUN wget https://releases.hashicorp.com/packer/1.5.1/packer_1.5.1_linux_amd64.zip
RUN unzip packer_1.5.1_linux_amd64.zip && rm packer_1.5.1_linux_amd64.zip
RUN mv packer /bin


# install terraform
RUN wget https://releases.hashicorp.com/terraform/0.12.18/terraform_0.12.18_linux_amd64.zip
RUN unzip terraform_0.12.18_linux_amd64.zip && rm terraform_0.12.18_linux_amd64.zip
RUN mv terraform /bin


ENTRYPOINT [ "bash" ]