FROM ubuntu:17.10
LABEL maintainer="guilhermebresser <guilhermebresser@gmail.com>"

RUN apt-get update
RUN apt-get install -y zip php php-xml php-mcrypt php-pdo-mysql php-mbstring python python-pip composer
RUN pip install boto3==1.3.0

WORKDIR /var/www 