#Based from Alpine 3.7
FROM alpine:3.7

#Install needed apps
RUN apk update
RUN apk add python python3 git

#Get project from github
RUN git clone https://github.com/jamckee/amazon-alexa-lg-tv

#Enable PIP
RUN python -m ensurepip --default-pip
RUN pip install -r /amazon-alexa-lg-tv/requirements.txt

#install python3 and PIP requirements
RUN apk add python3
RUN python3 -m pip install -r /amazon-alexa-lg-tv/requirements.txt
