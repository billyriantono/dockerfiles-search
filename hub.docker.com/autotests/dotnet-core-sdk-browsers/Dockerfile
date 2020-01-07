FROM mcr.microsoft.com/dotnet/core/sdk:2.1

# Install Java 11 LTS / OpenJDK 11
RUN if grep -q Debian /etc/os-release && grep -q stretch /etc/os-release; then \
		  echo 'deb http://deb.debian.org/debian stretch-backports main' | tee -a /etc/apt/sources.list.d/stretch-backports.list; \
	  elif grep -q Ubuntu /etc/os-release && grep -q xenial /etc/os-release; then \
		  apt-get update && apt-get install -y software-properties-common && \
		  add-apt-repository -y ppa:openjdk-r/ppa; \
	  fi && \
	    apt-get update && apt-get install -y openjdk-11-jre openjdk-11-jre-headless openjdk-11-jdk openjdk-11-jdk-headless && \
	    apt-get install -y bzip2 libgconf-2-4 # for extracting firefox and running chrome, respectively

# Install FireFox
RUN FIREFOX_URL="https://download.mozilla.org/?product=firefox-latest-ssl&os=linux64&lang=en-US" \
    && ACTUAL_URL=$(curl -Ls -o /dev/null -w %{url_effective} $FIREFOX_URL) \
    && curl --silent --show-error --location --fail --retry 3 --output /tmp/firefox.tar.bz2 $ACTUAL_URL \
    && tar -xvjf /tmp/firefox.tar.bz2 -C /opt \
    && ln -s /opt/firefox/firefox /usr/local/bin/firefox \
    && apt-get install -y libgtk3.0-cil-dev libasound2 libasound2 libdbus-glib-1-2 libdbus-1-3 \
    && rm -rf /tmp/firefox.* \
    && firefox --version

# Install Google Chrome
RUN curl --silent --show-error --location --fail --retry 3 --output /tmp/google-chrome-stable_current_amd64.deb https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb \
    && (dpkg -i /tmp/google-chrome-stable_current_amd64.deb || apt-get -fy install)  \
    && rm -rf /tmp/google-chrome-stable_current_amd64.deb \
    && sed -i 's|HERE/chrome"|HERE/chrome" --disable-setuid-sandbox --no-sandbox|g' \
        "/opt/google/chrome/google-chrome" \
    && google-chrome --version

# Start xvfb automatically
ENV DISPLAY :99
RUN printf '#!/bin/sh\nXvfb :99 -screen 0 1280x1024x24 &\nexec "$@"\n' > /tmp/entrypoint \
    && chmod +x /tmp/entrypoint \
    && mv /tmp/entrypoint /docker-entrypoint.sh

ENTRYPOINT ["/docker-entrypoint.sh"]
CMD ["/bin/sh"]