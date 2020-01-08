FROM ubuntu:16.04

# user mods for jenkins:
RUN groupadd -r seluser
RUN useradd --no-log-init -r -g seluser seluser
RUN usermod -u 639 seluser
RUN groupmod -g 639 seluser
RUN mkdir /home/seluser
RUN chown -R seluser:seluser /home/seluser
RUN su seluser

RUN cd /

# APT packages
RUN apt-get update
RUN apt-get install -yq curl python python3 python3-setuptools default-jdk unzip xvfb libxi6 libgconf-2-4 wget xz-utils nodejs jq

# sfdx
RUN wget https://developer.salesforce.com/media/salesforce-cli/sfdx-linux-amd64.tar.xz -O ./sfdx-linux-amd64.tar.xz
RUN mkdir sfdx
RUN tar -xJf ./sfdx-linux-amd64.tar.xz -C sfdx --strip-components 1
RUN ./sfdx/install
RUN rm -r ./sfdx-linux-amd64.tar.xz
RUN sfdx update

# chrome
RUN wget http://chromedriver.storage.googleapis.com/2.38/chromedriver_linux64.zip -O ./chromedriver_linux64.zip
RUN unzip ./chromedriver_linux64.zip && mv ./chromedriver /usr/local/bin/chromedriver
RUN chmod +x /usr/local/bin/chromedriver
RUN rm -r ./chromedriver_linux64.zip
RUN curl -sS -o - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add - && \
    echo "deb http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google-chrome.list && \
    apt-get -yqq update && \
    apt-get -yqq install google-chrome-stable && \
    rm -rf /var/lib/apt/lists/*

# python
RUN easy_install3 pip 
RUN pip install requests selenium webdriver_manager

# Permissions related to lightning tests
RUN mkdir /usr/local/lib/sfdx/node_modules/selenium-standalone/.selenium
RUN chown -R seluser:seluser /usr/local/lib/sfdx/node_modules/selenium-standalone/.selenium

ENTRYPOINT ["tail", "-f", "/dev/null"]
