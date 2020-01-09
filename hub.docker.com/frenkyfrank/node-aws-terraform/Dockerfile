FROM node:8.1.0

RUN apt-get update && apt-get install -y \
    python-dev \
    zip \
    git \
    jq

RUN curl -O https://bootstrap.pypa.io/get-pip.py

RUN python get-pip.py
RUN pip install awscli

RUN wget -O terraform.zip  "https://releases.hashicorp.com/terraform/0.11.8/terraform_0.11.8_linux_amd64.zip" && \
    unzip terraform.zip -d /bin && \
    rm -rf terraform.zip

CMD ["node"]