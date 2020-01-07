FROM node:9

ENV HUGO_VERSION 0.31.1

# Install awscli
RUN apt update && apt install -y python-dev && rm -rf /var/lib/apt/lists/* && \
    curl -O https://bootstrap.pypa.io/get-pip.py && \
    python get-pip.py --user && \
    ~/.local/bin/pip install awscli

# Install gulp
RUN npm install gulp

# Install hugo
RUN curl -L -O https://github.com/gohugoio/hugo/releases/download/v0.31.1/hugo_${HUGO_VERSION}_Linux-64bit.deb && \
    dpkg -i hugo_${HUGO_VERSION}_Linux-64bit.deb && \
    rm hugo_${HUGO_VERSION}_Linux-64bit.deb
