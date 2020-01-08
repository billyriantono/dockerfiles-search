FROM circleci/node:10-browsers

RUN sudo apt-get update 
RUN sudo apt-get install -yq --no-install-recommends libasound2 libatk1.0-0 libc6 libcairo2 libcups2 libdbus-1-3 libexpat1 libfontconfig1 libgcc1 libgconf-2-4 libgdk-pixbuf2.0-0 libglib2.0-0 libgtk-3-0 libnspr4 libpango-1.0-0 libpangocairo-1.0-0 libstdc++6 libx11-6 libx11-xcb1 libxcb1 libxcursor1 libxdamage1 libxext6 libxfixes3 libxi6 libxrandr2 libxrender1 libxss1 libxtst6 libnss3

WORKDIR /tmp

# Download ChromeDriver v.79.0.3945.36 manually. The most recent version of chromeDriver provided by webdriver-manager is 75.
RUN wget https://chromedriver.storage.googleapis.com/79.0.3945.36/chromedriver_linux64.zip
RUN unzip chromedriver_linux64.zip

# _XSERVTransmkdir: ERROR: euid != 0,directory /tmp/.X11-unix will not be created.
#
# 1. mkdir /tmp/.X11-unix (make a directory)
# 2. sudo chmod a+rwx /tmp/.X11-unix (give it all rights)
RUN mkdir /tmp/.X11-unix && \
    chmod 1777 /tmp/.X11-unix
	
WORKDIR /protractor