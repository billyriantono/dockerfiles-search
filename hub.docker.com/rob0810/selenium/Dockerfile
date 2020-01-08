FROM node:8.3

RUN apt-get update && apt-get install -yq  firefox-esr chromium git-core xvfb xsel unzip libgconf2-4 libncurses5 libxml2-dev libxslt-dev libz-dev xclip

RUN wget -q "https://github.com/mozilla/geckodriver/releases/download/v0.19.1/geckodriver-v0.19.1-linux64.tar.gz" -O /tmp/geckodriver.tgz && tar zxf /tmp/geckodriver.tgz -C /usr/bin/ && rm /tmp/geckodriver.tgz                                     

RUN wget -q "https://chromedriver.storage.googleapis.com/2.45/chromedriver_linux64.zip" -O /tmp/chromedriver.zip && unzip /tmp/chromedriver.zip -d /usr/bin/ && rm /tmp/chromedriver.zip                                              

ADD xvfb-chromium /usr/bin/xvfb-chromium

RUN ln -s /usr/bin/xvfb-chromium /usr/bin/google-chrome && chmod 777 /usr/bin/xvfb-chromium

RUN ln -s /usr/bin/geckodriver /usr/bin/chromium-browser && chmod 777 /usr/bin/geckodriver && chmod 777 /usr/bin/chromium-browser                                                                                                                                                                                                                                    

RUN npm install -g protractor && webdriver-manager update

RUN webdriver-manager update --versions.chrome=2.28 --gecko=false --standalone=false

# WORKDIR /test
# ADD conf.js /test/conf.js
# ADD test-spec.js /test/test-spec.js
# RUN xvfb-run --server-args="-screen 0 1024x768x24" -a protractor conf.js