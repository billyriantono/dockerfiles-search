FROM selenium/node-chrome-debug

USER root

RUN apt-get update && apt-get install -y software-properties-common
RUN add-apt-repository universe
RUN apt-get update && apt-get install -y python3.7

RUN ln -s -f /usr/bin/python3.7 /usr/bin/python3    

RUN apt-get install -y python3-venv

RUN apt-get install -y python3-pip

USER seluser

#====================================
# Scripts to run Selenium Standalone
#====================================
COPY config/start-selenium-standalone.sh /opt/bin/start-selenium-standalone.sh

#==============================
# Supervisor configuration file
#==============================
COPY config/selenium.conf /etc/supervisor/conf.d/
COPY config/selenium-debug.conf /etc/supervisor/conf.d/


RUN pip3 install selenium

WORKDIR /dev/shm

EXPOSE 4444
EXPOSE 5900