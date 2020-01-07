FROM python:3.7

# install google chrome
RUN wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add -
RUN sh -c 'echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google-chrome.list'
RUN apt-get -y update
RUN apt-get install -y google-chrome-stable

# install chromedriver
RUN apt-get install -yqq unzip
RUN wget -O /tmp/chromedriver.zip http://chromedriver.storage.googleapis.com/`curl -sS chromedriver.storage.googleapis.com/LATEST_RELEASE`/chromedriver_linux64.zip
RUN unzip /tmp/chromedriver.zip chromedriver -d /usr/local/bin/

# set display port to avoid crash
ENV DISPLAY=:99

# install selenium and other packages
RUN pip install selenium==3.13.0
RUN pip install civis==1.10.0
RUN pip install boto3==1.9.159
RUN pip install bs4==0.0.1
RUN pip install geopy==1.20.0
RUN pip install html5lib==1.0.1
RUN pip install twython==3.7.0
RUN pip install pandas==0.24.2
RUN pip install newsapi-python==0.2.5
RUN pip install xmltodict==0.12.0
RUN pip install pytrends==4.6.0
RUN pip install mysql.connector
RUN pip install ratelimit
RUN pip install parsons
RUN pip install git+https://github.com/bluestatedigital/bsd-api-python
RUN pip install postgis
