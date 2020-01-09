FROM trion/ng-cli:7.1.4

USER root

ADD xvfb-chromium /usr/bin/xvfb-chromium
ADD xvfb-chromium-webgl /usr/bin/xvfb-chromium-webgl
ADD display-chromium /usr/bin/display-chromium

RUN apt-get update \
    && apt-get install -y \
      xvfb sshpass \
      libosmesa6 \
      libgconf-2-4 default-jre wget libcairo2-dev libjpeg-dev libpango1.0-dev libgif-dev build-essential g++ tar \
 && wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb \
 && (dpkg -i google-chrome-stable_current_amd64.deb; apt-get -fy install; rm google-chrome-stable_current_amd64.deb; apt-get clean; rm -rf /var/lib/apt/lists/* ) \
 && mv /usr/bin/google-chrome /usr/bin/google-chrome.real  \
 && mv /opt/google/chrome/google-chrome /opt/google/chrome/google-chrome.real  \
 && rm /etc/alternatives/google-chrome \
 && ln -s /opt/google/chrome/google-chrome.real /etc/alternatives/google-chrome \
 && ln -s /usr/bin/xvfb-chromium /usr/bin/google-chrome \
 && ln -s /usr/bin/xvfb-chromium /usr/bin/chromium-browser \
 && ln -s /usr/lib/x86_64-linux-gnu/libOSMesa.so.6 /opt/google/chrome/libosmesa.so

RUN npm install -g npm-install-peers
USER $USER_ID
CMD "/bin/bash"
