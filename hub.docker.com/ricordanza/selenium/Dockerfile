FROM ricordanza/develop

# Enviroment setting
ENV DEBIAN_FRONTEND=noninteractive \
	PYTHONIOENCODING=utf-8
RUN ln -sf /bin/bash /bin/sh

# Basic apps
RUN apt-get update -y 
RUN apt-get install -y software-properties-common vim curl wget zip git python3-pip
RUN apt-get install -y language-pack-ja-base language-pack-ja fonts-ipaexfont-gothic fonts-ipafont-gothic

# Localization
RUN update-locale LANG=ja_JP.UTF-8 LANGUAGE="ja_JP:ja"
RUN apt-get install -y tzdata
RUN ln -sf /usr/share/zoneinfo/Asia/Tokyo /etc/localtime
RUN ln -sf /usr/bin/pip3 /usr/bin/pip
RUN ln -sf /usr/bin/python3 /usr/bin/python

# Selenium
RUN pip install selenium

# Chrome Driver 
RUN sh -c 'echo "deb http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google.list'
RUN wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add -
RUN apt-get update -y && apt-get install -y google-chrome-stable
RUN CHROME_DRIVER_VERSION=`curl -sS chromedriver.storage.googleapis.com/LATEST_RELEASE` && \
	wget -N http://chromedriver.storage.googleapis.com/$CHROME_DRIVER_VERSION/chromedriver_linux64.zip -P ~/
RUN unzip ~/chromedriver_linux64.zip -d ~/
RUN rm ~/chromedriver_linux64.zip
RUN chown root:root ~/chromedriver
RUN chmod 755 ~/chromedriver
RUN mv ~/chromedriver /usr/bin/chromedriver 

# Firefox Driver
RUN apt-add-repository -y ppa:mozillateam/firefox-next
RUN apt-get update -y
RUN apt-get install -y firefox
RUN GECKO_DRIVER_URL=$(curl -s https://api.github.com/repos/mozilla/geckodriver/releases/latest | python -c "import sys, json; print(next(item['browser_download_url'] for item in json.load(sys.stdin)['assets'] if 'linux64' in item.get('browser_download_url', '')))")  && \
	wget -N $GECKO_DRIVER_URL -P ~/
RUN tar -zxvf ~/geckodriver-*-linux64.tar.gz -C ~/
RUN rm -f ~/geckodriver-*-linux64.tar.gz 
RUN chown root:root ~/geckodriver
RUN chmod 755 ~/geckodriver
RUN mv ~/geckodriver /usr/bin/geckodriver 

# Clean
RUN apt-get autoremove
RUN apt-get autoclean
RUN apt-get clean
RUN rm -rf /var/lib/apt/lists/*
RUN rm -rf /var/cache/apt/*
RUN rm -rf /var/log/*
