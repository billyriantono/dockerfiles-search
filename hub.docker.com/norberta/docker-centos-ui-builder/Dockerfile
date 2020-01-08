FROM centos:7

USER root

# Create Google Chrome repository
RUN CHROME_REPO=/etc/yum.repos.d/google-chrome.repo && \
    echo '[google-chrome]' >> $CHROME_REPO && \
    echo 'name=google-chrome' >> $CHROME_REPO && \
    echo 'baseurl=http://dl.google.com/linux/chrome/rpm/stable/$basearch' >> $CHROME_REPO && \
    echo 'enabled=1' >> $CHROME_REPO && \
    echo 'gpgcheck=1' >> $CHROME_REPO && \
    echo 'gpgkey=https://dl-ssl.google.com/linux/linux_signing_key.pub' >> $CHROME_REPO

# Set up repository for latest NodeJS
RUN NODE_REPO=https://rpm.nodesource.com/setup_7.x && \
    curl --silent --location $NODE_REPO | bash -

# Install packages
RUN yum update -y && \
    yum -y install \
    google-chrome-stable \
    liberation-mono-fonts \
    liberation-narrow-fonts \
    liberation-sans-fonts \
    liberation-serif-fonts \
    xorg-x11-server-Xvfb \
    nodejs && \
    yum clean all && \
    npm install npm@latest -g

# Set up D-Bus Library
RUN dbus-uuidgen > /etc/machine-id

# Create symlink for Google Chrome which runs it without sandbox
ADD chrome-default /usr/local/bin/chrome-default
RUN chmod +x /usr/local/bin/chrome-default
RUN ln -sf /usr/local/bin/chrome-default /usr/bin/google-chrome

# Create Xvfb start script
ENV SCREEN_WIDTH 1920
ENV SCREEN_HEIGHT 1080
ENV SCREEN_DEPTH 16
ENV DISPLAY :99
ENV GEOMETRY "$SCREEN_WIDTH""x""$SCREEN_HEIGHT""x""$SCREEN_DEPTH"

ADD xvfb-start /usr/local/bin/xvfb-start
RUN chmod +x /usr/local/bin/xvfb-start

# Create script for entrypoint
ADD entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh

ENTRYPOINT ["/entrypoint.sh"]