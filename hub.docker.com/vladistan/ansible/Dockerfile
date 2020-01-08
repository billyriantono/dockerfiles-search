FROM python:3.7

RUN pip install ansible botocore boto3
RUN wget --quiet -O packer.zip https://releases.hashicorp.com/packer/1.4.1/packer_1.4.1_linux_amd64.zip && \
    unzip packer.zip && \
    mv packer /usr/bin && \
    rm packer.zip
