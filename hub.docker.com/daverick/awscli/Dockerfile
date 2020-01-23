FROM python:3.6

RUN adduser --disabled-login --gecos '' aws
VOLUME /home/aws

RUN mkdir -p /awscli
VOLUME /awscli
WORKDIR /awscli

#installing nodejs
RUN curl -sL https://deb.nodesource.com/setup_6.x | bash && \
    apt-get install -y --no-install-recommends nodejs


#installing serverless framework
RUN npm install -g serverless

COPY requirements.txt /tmp
RUN pip install --no-cache-dir -r /tmp/requirements.txt

RUN apt-get update && apt-get install -y --no-install-recommends \
  groff 

USER aws

ENTRYPOINT ["aws"]
