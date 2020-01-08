# use small node image
FROM node:alpine

# install git ca-certificates openssl openssh for CircleCI
# install jq for JSON parsing
RUN apk add --update --no-cache git openssh ca-certificates openssl jq gettext xmlstarlet curl python3 py3-setuptools chromium

# install latest sfdx from npm
RUN npm install sfdx-cli --global
RUN sfdx --version
RUN sfdx plugins --core

# install ChromeDriver
RUN wget http://chromedriver.storage.googleapis.com/2.38/chromedriver_linux64.zip -O ./chromedriver_linux64.zip
RUN unzip ./chromedriver_linux64.zip && mv ./chromedriver /usr/local/bin/chromedriver
RUN chmod +x /usr/local/bin/chromedriver
RUN rm -r ./chromedriver_linux64.zip

# python
RUN echo "**** install pip ****" && \
    python3 -m ensurepip && \
    rm -r /usr/lib/python*/ensurepip && \
    pip3 install --no-cache --upgrade requests selenium webdriver_manager && \
    if [ ! -e /usr/bin/pip ]; then ln -s pip3 /usr/bin/pip ; fi

RUN python3 -V
RUN pip3 --version

RUN ln -s /usr/bin/chromium-browser /usr/bin/google-chrome
