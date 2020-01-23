FROM alpine:latest
USER root

#install awscli
RUN apk add --update python3 && \
    rm /var/cache/apk/* && \
    apk add unzip && \
    apk add curl && \
    apk add wget && \
    apk add jq
RUN pip3 install awscli
RUN aws configure set preview.cloudfront true

#install kubectl
RUN curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl
RUN chmod +x ./kubectl
RUN mv ./kubectl /usr/bin/kubectl

#install terraform
RUN wget https://releases.hashicorp.com/terraform/0.12.3/terraform_0.12.3_linux_amd64.zip
RUN unzip terraform_0.12.3_linux_amd64.zip
RUN chmod +x ./terraform
RUN mv ./terraform /usr/bin/terraform

WORKDIR /usr/src/build

CMD ["/bin/bash"]