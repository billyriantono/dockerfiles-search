FROM gocd/gocd-agent-alpine-3.10:v19.10.0

USER root 
RUN apk --no-cache upgrade && apk add --no-cache unzip openrc acl shadow 
WORKDIR /home 
RUN wget https://releases.hashicorp.com/terraform/0.12.17/terraform_0.12.17_linux_amd64.zip && unzip terraform_0.12.17_linux_amd64.zip && mv terraform /usr/local/bin/ && rm -f terra* 
RUN apk add docker && rc-update add docker boot
WORKDIR /go 
