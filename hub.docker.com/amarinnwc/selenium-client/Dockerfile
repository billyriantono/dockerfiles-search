FROM lalyos/ubuntu-desktop

#RUN apt-get update && \
#    apt-get install -y --no-install-recommends ubuntu-desktop && \
#    apt-get install -y gnome-panel gnome-settings-daemon metacity nautilus gnome-terminal

RUN apt-get update
RUN apt-get install -y wget nano unzip
RUN apt-get install -y gdebi
#RUN apt-get install -y openjdk-8-jre-headless
RUN apt-get install -y python-tk
RUN apt-get install -y python-pip

RUN pip install --upgrade pip

RUN pip install urllib3


# Install Python Selenium
RUN pip install -U selenium==3.3.1
RUN pip install robotframework-selenium2library

RUN cd /usr/src

# Install Google Chrome Statble
RUN wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
RUN gdebi -n google-chrome-stable_current_amd64.deb

# Install Firefox 52
RUN wget https://archive.mozilla.org/pub/firefox/releases/52.0.2/linux-x86_64/en-US/firefox-52.0.2.tar.bz2
RUN tar xvjf firefox-52.0.2.tar.bz2
RUN cp firefox/firefox /usr/bin/firefox
RUN chmod +x /usr/bin/firefox

# Install geckodriver 0.11.1
RUN wget https://github.com/mozilla/geckodriver/releases/download/v0.11.1/geckodriver-v0.11.1-linux64.tar.gz
RUN tar xfz geckodriver-v0.11.1-linux64.tar.gz
RUN cp geckodriver /usr/bin/
RUN chmod +x /usr/bin/geckodriver

# Install chrome driver 2.9
RUN wget http://chromedriver.storage.googleapis.com/2.9/chromedriver_linux64.zip
RUN unzip chromedriver_linux64.zip
RUN cp chromedriver /usr/bin/
RUN chmod +x /usr/bin/chromedriver

EXPOSE 5901
