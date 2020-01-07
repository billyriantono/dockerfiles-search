FROM python:3.6

RUN pip install -i http://pypi.douban.com/simple --trusted-host pypi.douban.com numpy && pip install scrapy && pip install mysql-connector
RUN apt-get update && apt-get -q -y --force-yes install tesseract-ocr && pip install pytesseract
RUN pip uninstall -y  Pillow && pip install Pillow==5.2.0
RUN pip install baidu-aip && pip install py3Fdfs
RUN pip install redis


# install google chrome
RUN wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add -
RUN sh -c 'echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google-chrome.list'
RUN apt-get -y update
RUN apt-get install -y google-chrome-stable

# install chromedriver
RUN apt-get install -yqq unzip
RUN wget -O /tmp/chromedriver.zip http://chromedriver.storage.googleapis.com/`curl -sS chromedriver.storage.googleapis.com/LATEST_RELEASE`/chromedriver_linux64.zip
RUN unzip /tmp/chromedriver.zip chromedriver -d /usr/local/bin/

RUN apt-get install -y ttf-wqy-microhei ttf-wqy-zenhei xfonts-wqy
# set display port to avoid crash
ENV DISPLAY=:99

# install selenium
RUN pip install selenium==3.8.0

CMD ["python3"]