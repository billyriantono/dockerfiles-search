FROM python:3.7.3

MAINTAINER Takuya Nakagawa <takuya.nakagawa@netapp.com>

RUN groupadd demo
RUN useradd -d /home/bottle -m bottle

RUN pip install bottle
RUN pip install boto3
RUN pip install jinja2
RUN pip install urllib3

WORKDIR /home/bottle
RUN git clone https://github.com/tnak160521/aiq-api-demo01.git

EXPOSE 8080
ENTRYPOINT ["/usr/local/bin/python", "/home/bottle/aiq-api-demo01/demo.py"]
USER bottle
