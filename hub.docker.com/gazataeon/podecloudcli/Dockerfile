FROM badgerati/pode:1.0.1

# Update apt and install curl
RUN apt-get update && apt-get install curl -y

#Update python and Pip
RUN apt-get install python3 -y
RUN apt-get install python3-pip -y
RUN pip3 install --upgrade pip

# Install AZ CLI
RUN curl -sL https://aka.ms/InstallAzureCLIDeb | bash

# Install AWS CLI + S3CMD
RUN pip3 install awscli --upgrade --user
RUN apt-get install s3cmd -y