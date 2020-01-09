FROM python:3.6-slim
MAINTAINER Alek Hrycaiko "alek@sokanu.com"
WORKDIR /app
RUN apt-get update
RUN pip3 install rq-dashboard==0.3.12 
EXPOSE 9181
CMD ["rq-dashboard"]
 
