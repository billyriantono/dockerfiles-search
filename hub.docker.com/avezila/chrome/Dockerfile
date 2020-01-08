FROM ubuntu:devel

RUN \
    echo 'APT::Install-Recommends "false";' > /etc/apt/apt.conf.d/99synaptic \
 && echo 'path-exclude /usr/share/doc/*' >> /etc/dpkg/dpkg.cfg.d/01_nodoc \
 && echo 'path-exclude /usr/share/man/*' >> /etc/dpkg/dpkg.cfg.d/01_nodoc \
 && echo 'path-exclude /usr/share/groff/*' >> /etc/dpkg/dpkg.cfg.d/01_nodoc \
 && echo 'path-exclude /usr/share/info/*' >> /etc/dpkg/dpkg.cfg.d/01_nodoc \
 && echo 'path-exclude /usr/share/lintian/*' >> /etc/dpkg/dpkg.cfg.d/01_nodoc \
 && echo 'path-exclude /usr/share/linda/*' >> /etc/dpkg/dpkg.cfg.d/01_nodoc \
 && apt-get update \
 && apt-get install --no-install-recommends --no-install-suggests -y \
    wget unzip xvfb \
    libpangocairo-1.0-0 \
    libxcomposite1 \
    libx11-xcb1 \
    libxcursor1 \
    libxdamage1 \
    libxi6  \
    libxtst6 \
    libnss3 \
    libcups2 \
    libxss1 \
    libxrandr2 \
    libgconf2-4 \
    libasound2 \
    libatk1.0-0 \
    libgtk-3-0 \
&& cd ~ \
&& wget --no-check-certificate -O chrome-linux.zip "https://www.googleapis.com/download/storage/v1/b/chromium-browser-snapshots/o/Linux_x64%2F484882%2Fchrome-linux.zip?generation=1499425907683280&alt=media" \
&& unzip chrome-linux.zip \
&& mv chrome-linux /chrome \
&& rm chrome-linux.zip \
&& mkdir -p /usr/lib/chromium/ \
&& echo '/chrome/chrome --headless --no-sandbox --disable-gpu --start-maximized' > /usr/lib/chromium/chromium \
&& chmod +x /usr/lib/chromium/chromium \
&& wget --no-check-certificate -O chromedriver.zip "https://chromedriver.storage.googleapis.com/2.30/chromedriver_linux64.zip" \
&& unzip chromedriver.zip \
&& mv ./chromedriver /bin/ \
&& rm chromedriver.zip \
&& apt-get -y purge wget \
&& apt-get -y autoremove \
&& apt-get clean \
&& rm -rf \
    /tmp/* \
    /usr/share/doc/* \
    /var/cache/* \
    /var/lib/apt/lists/* \
    /var/tmp/* \
&& ln -s /chrome/chrome /bin/chrome

RUN \
    echo '#!/bin/sh' >> /run.sh \
 && echo 'export DISPLAY=:1' >> /run.sh \
 && echo 'Xvfb $DISPLAY -ac -screen 0 1280x1024x8 &' >> /run.sh \
 && echo 'sleep 1' >> /run.sh \
 && echo 'xvfb-run $@' >> /run.sh \
 && chmod +x /run.sh

EXPOSE 4444

CMD ["/run.sh", "chromedriver", "--args", "['start-maximized', 'disable-web-security','headless', 'no-sandbox', 'disable-gpu']", "--binary", "/chrome/crhome", "--url-base=/wd/hub", "--port=4444", "--whitelisted-ips=''"]

