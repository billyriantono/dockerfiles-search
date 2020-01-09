FROM google/cloud-sdk:alpine
ENV TF_VERSION 0.10.2

# Install terraform
RUN curl -sSL https://releases.hashicorp.com/terraform/${TF_VERSION}/terraform_${TF_VERSION}_linux_amd64.zip -o /tmp/terraform.zip && \
       unzip /tmp/terraform.zip -d /usr/bin && rm -rf /tmp/*

# Create unprivileged user
RUN adduser -Du 1000 user

VOLUME ["/home/user", "/data"]
WORKDIR /data
USER 1000:1000
