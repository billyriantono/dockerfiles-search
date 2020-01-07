FROM ubuntu:latest
MAINTAINER Sakharam Thorat <srt.2011@outlook.com>

RUN apt-get update && apt-get install -y --no-install-recommends apt-utils
RUN apt-get update
RUN apt-get install -y python-pip python-dev gcc phantomjs
RUN pip install robotframework
RUN pip install pycrypto

RUN apt-get install -y build-essential libssl-dev libffi-dev python-dev
RUN pip install robotframework-sshlibrary
RUN pip install robotframework-selenium2library


RUN apt-get install -y wget
RUN apt-get install -y firefox 
RUN apt-get install -y xvfb

# Install geckodriver
RUN wget https://github.com/mozilla/geckodriver/releases/download/v0.20.1/geckodriver-v0.20.1-linux64.tar.gz
RUN tar xvf geckodriver-v0.20.1-linux64.tar.gz
RUN cp geckodriver /usr/bin/

ENV ROBOT_TESTS /robots/

ADD run.sh /usr/local/bin/run.sh
RUN chmod +x /usr/local/bin/run.sh

CMD ["run.sh"]

