FROM selenium/standalone-chrome
USER root

RUN export
#RUN apt-get -y install apt-transport-https
RUN apt-get update
RUN apt-get -y install python3
#RUN apt-get -y install python3-pip
RUN python --version

WORKDIR /app

COPY . /app

RUN python app/get-pip.py
RUN pip install --trusted-host pypi.python.org -r app/requirements.txt