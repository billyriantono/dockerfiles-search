FROM node:8.9-slim

# List of required Chrome dependencies found in this page > google-chrome-stable : https://deb.pkgs.org/universal/google-amd64/ 
ARG CHROME_DEPS="ca-certificates dpkg fonts-liberation libappindicator3-1 libasound2 libatk-bridge2.0-0 libatk1.0-0 libc6 libcairo2 libcups2 libdbus-1-3 libexpat1 libgcc1 libgdk-pixbuf2.0-0 libglib2.0-0 libgtk-3-0 libnspr4 libnss3 libpango-1.0-0 libpangocairo-1.0-0 libstdc++6 libuuid1 libx11-6 libx11-xcb1 libxcb1 libxcomposite1 libxcursor1 libxdamage1 libxext6 libxfixes3 libxi6 libxrandr2 libxrender1 libxss1 libxtst6 lsb-release wget xdg-utils"

# Install tools 
RUN apt-get update && apt-get install -y make wget git $CHROME_DEPS --no-install-recommends

# Download Chrome stable v71.0
RUN wget -O google-chrome.deb https://www.slimjet.com/chrome/download-chrome.php?file=files/71.0.3578.80/google-chrome-stable_current_amd64.deb

# Install Chrome
RUN dpkg -i ./google-chrome.deb

# Clean install files
RUN rm -f ./google-chrome.deb \
    rm -rf /var/lib/apt/lists/* \
    && rm -rf /src/*.deb

# Tell Puppeteer to not download his own Google Chrome build
ENV PUPPETEER_SKIP_CHROMIUM_DOWNLOAD=true
