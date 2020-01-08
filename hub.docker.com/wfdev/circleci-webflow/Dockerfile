FROM node:6.10.0

ENV DOCKER_VERSION "17.03.0-ce"
ENV PYTHONIOENCODING=UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

RUN \
  # Add Chrome repository
  wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add - && \
  echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google-chrome.list && \

  # Update packages
  apt-get update -qq && \

  # Install packages
  apt-get install -qy --no-install-recommends \
    google-chrome-stable \
    less \
    locales \
    man \
    netcat \
    python \
    python-dev \
    python-pip \
    ssh \
    unzip \
    xvfb \
    && \

  # Set locale
  echo "en_US.UTF-8 UTF-8" | tee -a /etc/locale.gen && \
  locale-gen && \
  update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8 && \

  # Install awscli
  pip install --upgrade pip awscli && \

  # Set Chrome options
  sed -i 's|HERE/chrome"|HERE/chrome" --disable-setuid-sandbox --no-sandbox|g' "/opt/google/chrome/google-chrome" && \

  # Install chromedriver
  wget https://chromedriver.storage.googleapis.com/2.27/chromedriver_linux64.zip && \
  unzip chromedriver_linux64.zip && \
  chmod +x chromedriver && \
  mv chromedriver /usr/local/bin/chromedriver && \
  rm chromedriver_linux64.zip && \

  # Configure Container
  git config --global user.name "CircleCI" && \
  git config --global user.email "tech@webflow.com" && \
  npm set progress=false && \
  yarn global add node-gyp && \

  # Add Docker CLI tool
  curl -L -o /tmp/docker-$DOCKER_VERSION.tgz https://get.docker.com/builds/Linux/x86_64/docker-$DOCKER_VERSION.tgz && \
  tar -xz -C /tmp -f /tmp/docker-$DOCKER_VERSION.tgz && \
  mv /tmp/docker/* /usr/bin && \

  # Cleanup
  apt-get autoremove -y && \
  apt-get clean -y && \
  rm -rf /tmp/* /var/tmp/* /var/lib/apt/lists/* /var/cache/* /root/.cache/*

VOLUME /app
WORKDIR /app
