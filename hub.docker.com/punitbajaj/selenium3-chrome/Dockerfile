FROM debian:stable

RUN apt-get update && apt-get install -y curl xvfb chromium python python-pip curl unzip libgconf-2-4 vim procps wget

ADD xvfb-chromium /usr/bin/xvfb-chromium
RUN ln -s /usr/bin/xvfb-chromium /usr/bin/google-chrome
RUN ln -s /usr/bin/xvfb-chromium /usr/bin/chromium-browser

ENV CHROMEDRIVER_VERSION 2.42

RUN curl -SLO "https://chromedriver.storage.googleapis.com/$CHROMEDRIVER_VERSION/chromedriver_linux64.zip" \
  && unzip "chromedriver_linux64.zip" -d /usr/local/bin \
  && rm "chromedriver_linux64.zip"

RUN pip install pytest selenium easyprocess itsdangerous robotframework robotframework-pabot robotframework-seleniumlibrary PyVirtualDisplay \
                pyaml robotframework-imaplibrary robotframework-debuglibrary mechanize python-dateutil beautifulsoup4 python-guerrillamail pyparsing


RUN mkdir /automationDIR
WORKDIR /



