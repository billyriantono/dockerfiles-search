FROM ubuntu:18.04

# Update apt  
RUN apt-get update 

#Update python and Pip
RUN apt-get install python -y
RUN apt-get install python-pip -y
RUN pip install --upgrade pip

# Install AWS CLI + S3CMD
RUN pip install awscli --upgrade --user
RUN pip install s3cmd 
