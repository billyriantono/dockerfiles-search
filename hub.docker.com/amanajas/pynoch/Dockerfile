FROM python

RUN pip3 install --upgrade pip

RUN pip3 install nodejs

# Chromedriver missing libs
RUN apt-get -yqq update
RUN apt-get -yqq install libnss3 libgconf-2-4

# Install chrome
RUN apt-get install -y libxss1 libappindicator1 libindicator7
RUN wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
RUN apt install -y ./google-chrome*.deb
RUN apt-get install -f

# Install npm
RUN apt-get install -y npm
