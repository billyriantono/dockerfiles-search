FROM debian:buster-slim

RUN apt update
RUN apt dist-upgrade -y
RUN apt install -y python3-dev wget gnupg2 unzip

RUN wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add -
RUN echo 'deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main' | tee /etc/apt/sources.list.d/google-chrome.list

RUN apt update
RUN apt install -y google-chrome-stable
RUN wget "http://chromedriver.storage.googleapis.com/$(wget -O - http://chromedriver.storage.googleapis.com/LATEST_RELEASE)/chromedriver_linux64.zip" -O /tmp/chromedriver_linux64.zip
RUN unzip /tmp/chromedriver_linux64.zip -d /tmp
RUN rm /tmp/chromedriver_linux64.zip
RUN mv /tmp/chromedriver /usr/local/bin

RUN wget https://bootstrap.pypa.io/get-pip.py
RUN python3 get-pip.py
RUN rm get-pip.py
RUN pip3 install --upgrade pip wheel setuptools selenium
