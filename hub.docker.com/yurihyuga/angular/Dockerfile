FROM ubuntu:16.04
LABEL  maintainer "UrmnafBortHyuga <yurihyuga1889@gmail.com>"

RUN dpkg --add-architecture i386


# Install Packages
RUN apt-get update 
RUN apt-get install -y curl zip unzip git wget
# RUN apt-get install -y --no-install-recommends chromium-browser chromium-chromedriver
RUN wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add - 
RUN sh -c 'echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google.list'
RUN apt-get update
RUN apt-get install -y google-chrome-beta
RUN apt-get clean && rm -rf /var/lib/apt/list

# Install Node
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash -
RUN apt-get --quiet install --yes nodejs
RUN npm i -g @angular/cli

# Set up chromium
# ENV CHROME_BIN /usr/bin/chromium-browser
# ENV CHROMIUM_FLAGS "--disable-gpu --no-sandbox --headless"
# RUN ln -s /usr/lib/chromium-browser/chromedriver /usr/bin/
# RUN rm /etc/chromium-browser/default
