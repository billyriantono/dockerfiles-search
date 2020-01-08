FROM node:lts-stretch

# Handle SIGINT and others better.
RUN wget https://github.com/Yelp/dumb-init/releases/download/v1.2.0/dumb-init_1.2.0_amd64.deb \
  && dpkg -i dumb-init_*.deb \
  && rm dumb-init_*.deb

ENTRYPOINT ["dumb-init"]

# Install prereqs
RUN apt-get update \
  && apt-get install -y zip libdbus-glib-1-2 \
  # Install latest Chrome
  && wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add - \
  && echo 'deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main' | tee /etc/apt/sources.list.d/google-chrome.list \
  && apt-get update \
  && apt-get install google-chrome-stable dbus-x11 -y --no-install-recommends \
  # Install latest Firefox
  && wget -O /tmp/firefox.tar.bz2 'https://download.mozilla.org/?product=firefox-latest&os=linux64&lang=en-US' \
  && tar -C /opt -xjf /tmp/firefox.tar.bz2 \
  && rm /tmp/firefox.tar.bz2 \
  && ln -fs /opt/firefox/firefox /usr/bin/firefox \
  # Cleanup
  && apt-get autoremove --purge -y \
  && apt-get clean

RUN firefox -CreateProfile "headless /moz-headless" -headless
ADD ./user.js /moz-headless/user.js
RUN chmod -R a+rwx /moz-headless

ENV DBUS_SESSION_BUS_ADDRESS=/dev/null