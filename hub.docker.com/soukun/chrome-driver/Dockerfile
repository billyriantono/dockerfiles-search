FROM python:3
 
RUN apt-get update && apt-get install -y unzip
 
#install google-chrome
RUN wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add && \
    echo 'deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main' | tee /etc/apt/sources.list.d/google-chrome.list && \
    apt-get update && \
    apt-get install -y google-chrome-stable
 
#install selenium
RUN pip install selenium
RUN pip install bottle
RUN pip install bottledaemon
RUN pip install request
RUN pip install requests
RUN pip install beautifulsoup4
#install ChromeDriver
ADD https://chromedriver.storage.googleapis.com/74.0.3729.6/chromedriver_linux64.zip /opt/chrome/
RUN cd /opt/chrome/ && \
    unzip chromedriver_linux64.zip
 
ENV PATH /usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/opt/chrome
COPY server1.py /opt/chrome/
EXPOSE 8081
ENTRYPOINT ["python", "/opt/chrome/server1.py"]
