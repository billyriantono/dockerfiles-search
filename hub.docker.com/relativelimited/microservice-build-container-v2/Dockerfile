FROM amazonlinux
MAINTAINER Team Qubit <team-qubit@relative.uk.com>

RUN yum install -y python3-pip python3 python3-setuptools zip git procps
RUN curl -sL https://rpm.nodesource.com/setup_12.x | bash
RUN yum install -y nodejs
RUN pip3 install awscli
RUN pip3 install boto3
RUN npm install serverless typescript serverless-domain-manager expo-cli twilio-cli -g

CMD /bin/bash

