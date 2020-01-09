FROM circleci/node:10


RUN mkdir /home/circleci/setup_chrome
WORKDIR /home/circleci/setup_chrome

# Install headless chrome

RUN mkdir setup_chrome && cd setup_chrome

RUN wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | sudo apt-key add -

RUN sudo sh -c 'echo "deb http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google.list'

RUN sudo apt-get update

RUN sudo apt-get install google-chrome-stable

# Install chrome webdriver
#RUN curl https://chromedriver.storage.googleapis.com/LATEST_RELEASE -o LATEST_RELEASE

#RUN wget https://chromedriver.storage.googleapis.com/$(cat LATEST_RELEASE)/chromedriver_linux64.zip

# Japanese font
RUN sudo apt-get install fonts-ipafont