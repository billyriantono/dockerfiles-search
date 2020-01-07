FROM openjdk:8

RUN useradd -u 1000 -m -U webdriver

WORKDIR /home/webdriver
# Configure Xvfb via environment variables:
ENV SCREEN_WIDTH 1920
ENV SCREEN_HEIGHT 1080
ENV SCREEN_DEPTH 24

ENV DISPLAY=:99
ENV PATH="/usr/local/bin:${PATH}"

ADD entrypoint.sh /entrypoint.sh
# Install the latest versions of Google Chrome and Chromedriver:
RUN export DEBIAN_FRONTEND=noninteractive \
  && apt-get update \
  && apt-get install -y \
  unzip xvfb dbus   \
  && \
  DL=https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb \
  && curl -sL "$DL" > /tmp/chrome.deb \
  && apt install --no-install-recommends --no-install-suggests -y \
  /tmp/chrome.deb \
  && CHROMIUM_FLAGS='--no-sandbox --disable-dev-shm-usage' \
  # Patch Chrome launch script and append CHROMIUM_FLAGS to the last line:
  && sed -i '${s/$/'" $CHROMIUM_FLAGS"'/}' /opt/google/chrome/google-chrome \
  && BASE_URL=https://chromedriver.storage.googleapis.com \
  && VERSION=$(curl -sL "$BASE_URL/LATEST_RELEASE") \
  && curl -sL "$BASE_URL/$VERSION/chromedriver_linux64.zip" -o /tmp/driver.zip \
  && unzip /tmp/driver.zip \
  && mv chromedriver /usr/local/bin/ \
  && chmod -R 777 /usr/local/bin/ \
  && chmod -R 777 /opt/google/chrome \
  && chmod  777 /entrypoint.sh \
  # Remove obsolete files:
  && apt-get autoremove --purge -y \
  unzip \
  && apt-get clean \
  && rm -rf \
  /tmp/* \
  /usr/share/doc/* \
  /var/cache/* \
  /var/lib/apt/lists/* \
  /var/tmp/*

ENTRYPOINT ["/entrypoint.sh"]
