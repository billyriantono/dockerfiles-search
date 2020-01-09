FROM debian:stretch-slim

RUN apt update && apt dist-upgrade -y && apt install -y python3 wget gnupg2 unzip

ENV TZ=America/Denver
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add -
RUN echo 'deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main' | tee /etc/apt/sources.list.d/google-chrome.list

RUN apt update && apt install -y google-chrome-stable
RUN wget "http://chromedriver.storage.googleapis.com/$(wget -O - http://chromedriver.storage.googleapis.com/LATEST_RELEASE)/chromedriver_linux64.zip" -O /tmp/chromedriver_linux64.zip
RUN unzip /tmp/chromedriver_linux64.zip -d /tmp
RUN rm /tmp/chromedriver_linux64.zip
RUN mv /tmp/chromedriver /usr/local/bin

ADD requirements.txt requirements.txt

RUN wget https://bootstrap.pypa.io/get-pip.py
RUN python3 get-pip.py && rm get-pip.py && pip3 install --upgrade pip wheel setuptools --upgrade -r requirements.txt

ADD safeway.py safeway.py

# username and password for the safeway.py script should be set when running this container
# docker -e USERNAME='name' -e PASSWORD='pass' ...
# OR
# [Synology] set the environment variables in the run dialog
#
ENTRYPOINT ["sh", "-c", "while true; do python3 ./safeway.py; date; echo 'Run Complete, sleeping'; sleep 43200; done;"]
