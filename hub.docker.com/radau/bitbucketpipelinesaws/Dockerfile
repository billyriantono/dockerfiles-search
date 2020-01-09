FROM python:3.6.3

# Install Necessary Build dependencies 
RUN apt-get update && \
    apt-get install -y zip && \
    pip install awscli==1.11.182 boto3==1.3.0 botocore==1.8.11 && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
