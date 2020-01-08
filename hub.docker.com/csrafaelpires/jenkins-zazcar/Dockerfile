FROM jenkins

USER root

RUN apt-get update
RUN apt-get install -y jq
RUN apt-get clean
RUN curl -O https://bootstrap.pypa.io/get-pip.py
RUN python get-pip.py
RUN pip install boto3

USER jenkins
