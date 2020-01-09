FROM debian:stretch
RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y --no-install-recommends \
    autoconf \
    bison \
    build-essential \
    ca-certificates \
    curl \
    git-core \
    libcurl4-openssl-dev \
    libffi-dev \
    libgdbm3 \
    libgdbm-dev \
    libreadline-dev \
    libncurses5-dev \
    libsqlite3-dev \
    libssl-dev \
    libxml2-dev \
    libxslt1-dev \
    libyaml-dev \
    python \
    sqlite3 \
    zlib1g-dev imagemagick libmagickwand-dev libmariadbclient-dev fonts-vlgothic xvfb zip unzip

RUN git clone https://github.com/rbenv/rbenv.git /root/.rbenv && \
    git clone https://github.com/rbenv/ruby-build.git /root/.rbenv/plugins/ruby-build && \
 		git clone https://github.com/riywo/ndenv /root/.ndenv && \
    git clone https://github.com/riywo/node-build.git /root/.ndenv/plugins/node-build

ENV PATH /root/.rbenv/shims:/root/.rbenv/bin:/root/.ndenv/shims:/root/.ndenv/bin:$PATH


RUN rbenv install 2.5.1 && ndenv install 10.6.0 && rbenv global 2.5.1 && ndenv global 10.6.0
RUN curl -sSLo chrome.zip https://commondatastorage.googleapis.com/chromium-browser-snapshots/Linux_x64/549811/chrome-linux.zip && \
  unzip -q chrome.zip && \
  cp -R chrome-linux/* /usr/local/bin && \
  rm chrome.zip

RUN curl -sSLo chromedriver.zip https://chromedriver.storage.googleapis.com/2.35/chromedriver_linux64.zip && \
	unzip -q -d /usr/local/bin chromedriver.zip && \
	rm chromedriver.zip

