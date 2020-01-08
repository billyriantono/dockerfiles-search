FROM ruby:2.5.3

ENV APP_HOME /app
RUN mkdir $APP_HOME
WORKDIR $APP_HOME
ADD install_chrome_selenium.sh .

#upgrade ubuntu
RUN apt-get update
RUN apt-get install -y apt-utils whiptail build-essential

#set locale en_US.UTF-8
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y locales && \
    sed -i -e 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/' /etc/locale.gen && \
    dpkg-reconfigure --frontend=noninteractive locales && \
    update-locale LANG=en_US.UTF-8
ENV LANG en_US.UTF-8

RUN apt-get install -y libpq-dev libxml2-dev libxslt1-dev libqtwebkit4 \
                        libqt4-dev xvfb python python-dev python-pip python-virtualenv

# install latest nodejs 10.X
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash - && apt-get install -y nodejs

# install node packages
RUN npm install -g bower yarn phantomjs --unsafe-perm

# Install Chrome, ChromeDriver and Selenium
RUN bash install_chrome_selenium.sh

# cleanup
RUN rm -rf /var/lib/apt/lists/*

ONBUILD ADD . $APP_HOME

CMD ["bash"]