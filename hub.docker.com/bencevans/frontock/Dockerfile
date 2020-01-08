FROM markadams/chromium-xvfb-js

RUN apt-get update --fix-missing && apt-get upgrade -y
RUN apt-get install -y -q wget default-jre unzip bzip2 firefox-esr bsdtar

# Install BrowserStack Local Tunnel
RUN wget -qO- http://www.browserstack.com/browserstack-local/BrowserStackLocal-linux-x64.zip | bsdtar -xvf- -C /usr/local/bin/

CMD /bin/bash
