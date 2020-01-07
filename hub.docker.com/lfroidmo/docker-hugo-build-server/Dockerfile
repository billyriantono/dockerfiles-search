FROM ubuntu:16.04

RUN apt-get update -y 
RUN apt-get install -y npm \
    && apt-get install -y ruby-full \
    && apt-get install -y wget

# BOWER
RUN npm install -g bower && \
    echo '{ "allow_root": true }' > /root/.bowerrc

# SASS
RUN gem install sass

# HUGO
ENV HUGO_VERSION=0.16
RUN wget https://github.com/spf13/hugo/releases/download/v${HUGO_VERSION}/hugo_${HUGO_VERSION}_linux-64bit.tgz \
    && tar xzf hugo_${HUGO_VERSION}_linux-64bit.tgz \
    && rm -r hugo_${HUGO_VERSION}_linux-64bit.tgz \
    && mv hugo /usr/bin/hugo

CMD ["bash"]