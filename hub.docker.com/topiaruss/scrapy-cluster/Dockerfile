FROM python:2.7
MAINTAINER Madison Bahmer scrapy-cluster-tech@istresearch.com

# os setup
RUN apt-get update
RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

# install requirements
COPY utils /usr/src/app/utils
COPY requirements.txt /usr/src/app/
RUN pip install --no-cache-dir -r requirements.txt
RUN rm -rf /usr/src/utils

# move codebase over
COPY kafka-monitor /usr/src/app

# override settings via localsettings.py
COPY settings.py /usr/src/app/localsettings.py

# copy testing script into container
#COPY docker/run_docker_tests.sh /usr/src/app/run_docker_tests.sh

# set up environment variables

# run command
CMD ["python", "kafka_monitor.py", "run"]
