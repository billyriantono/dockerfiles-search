FROM ubuntu:trusty
ENV PUPPET_VERSION="3.8.7-1puppetlabs1"
ENV FACTER_VERSION="2.4.6-1puppetlabs1"
RUN apt-get update && apt-get install -y git ssh tar gzip ca-certificates curl wget ruby make ruby-dev git lsb-release perl unzip
RUN cd /tmp && wget https://apt.puppetlabs.com/puppetlabs-release-trusty.deb && dpkg -i puppetlabs-release-trusty.deb && apt-get update -q
RUN apt-get install -q -y puppet=${PUPPET_VERSION} facter=${FACTER_VERSION}
RUN apt-get update -q && apt-get autoremove -q -y

# Set the Chrome repo.
RUN wget -qO - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add - \
  && echo "deb http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google-chrome.list

# Install Chrome.
RUN apt-get update && apt-get -y install google-chrome-stable

# Install Chrome Driver
RUN google-chrome --version
RUN CHROME_VERSION=$(google-chrome --version | perl -pe's/Google Chrome (\d+\.\d+\.\d+).*/$1/') && \
    echo CHROME_VERSION=${CHROME_VERSION} && \
    CHROMEDRIVER_VERSION=$(curl https://chromedriver.storage.googleapis.com/LATEST_RELEASE_${CHROME_VERSION}) && \
    echo CHROMEDRIVER_VERSION=${CHROMEDRIVER_VERSION} && \
    CHROMEDRIVER_URL=https://chromedriver.storage.googleapis.com/${CHROMEDRIVER_VERSION}/chromedriver_linux64.zip && \
    echo CHROMEDRIVER_URL=${CHROMEDRIVER_URL} && \
    wget ${CHROMEDRIVER_URL} -O /tmp/chromedriver_linux64.zip && \
    ls -la /tmp/chromedriver_linux64.zip && \
    file /tmp/chromedriver_linux64.zip &&\
    (cd /tmp ; unzip /tmp/chromedriver_linux64.zip ) && \
    rm -f /tmp/chromedriver_linux64.zip && \
    mv /tmp/chromedriver /usr/local/bin/chromedriver

CMD ["/bin/cat"]
