FROM gocd/gocd-agent-alpine-3.7:v18.6.0

WORKDIR /

RUN   apk update \ 
 &&   apk add ca-certificates wget \  
 &&   update-ca-certificates 

RUN wget https://releases.hashicorp.com/terraform/0.11.7/terraform_0.11.7_linux_amd64.zip
RUN unzip /terraform_0.11.7_linux_amd64.zip
RUN mv /terraform /usr/bin/.
RUN chmod 775 /usr/bin/terraform
RUN rm /terraform_0.11.7_linux_amd64.zip
