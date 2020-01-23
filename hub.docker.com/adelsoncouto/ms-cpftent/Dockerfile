FROM python:3.5
LABEL maintainer "marcus.rickert@accso.de"

RUN apt-get update && \
    LC_ALL=C DEBIAN_FRONTEND=noninteractive apt-get install -y --force-yes --no-install-recommends \
         python3 \
         python3-pip \
	 python3-dev \
	 python3-wheel \
	 libxml2-dev \
 	 libxslt1-dev \
	 postgresql-client \
 	 libpq-dev \
	 git \
	 gcc \
	 g++ \
         apt-utils \
         curl \
	 wget \
	 expect \
         unzip \
         sshpass \
         openssh-client && \
    pip3 install codecov coverage jinja2 selenium && \
    curl -L https://chromedriver.storage.googleapis.com/2.46/chromedriver_linux64.zip -o /tmp/chromedriver_linux64.zip && \
    cd tmp && \
    unzip /tmp/chromedriver_linux64.zip && \
    mv /tmp/chromedriver /usr/local/bin && \
    curl -L https://www.slimjet.com/chrome/download-chrome.php?file=files%2F71.0.3578.80%2Fgoogle-chrome-stable_current_amd64.deb -o /tmp/google-chrome-stable_current_amd64.deb && \
    ( dpkg -i /tmp/google-chrome-stable_current_amd64.deb || true  ) && \
    LC_ALL=C DEBIAN_FRONTEND=noninteractive apt-get install -y --force-yes -f && \
    LC_ALL=C DEBIAN_FRONTEND=noninteractive apt-get clean
