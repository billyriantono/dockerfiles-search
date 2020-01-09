FROM php:7.0-apache

RUN docker-php-ext-install mysqli
RUN apt-get -y update && apt-get install -y build-essential libxss1 libappindicator1 libindicator7 wget
RUN wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add -
RUN sh -c 'echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google-chrome.list'
RUN apt-get update
RUN apt-get install -y google-chrome-stable xvfb unzip python-pip
RUN pip install pyvirtualdisplay selenium
RUN wget -N https://chromedriver.storage.googleapis.com/2.29/chromedriver_linux64.zip
RUN unzip chromedriver_linux64.zip
RUN chmod +x chromedriver
RUN mv -f chromedriver /usr/local/share/chromedriver
RUN ln -s /usr/local/share/chromedriver /usr/bin/chromedriver
RUN ln -s /usr/local/share/chromedriver /usr/local/bin/chromedriver
