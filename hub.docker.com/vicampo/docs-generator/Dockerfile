FROM ubuntu:17.10
ENV DEBIAN_FRONTEND noninteractive
COPY . /src
WORKDIR /src

RUN set -ex  \
  && apt-get update

# Install Python, pip and other utils
RUN set -ex \
  && apt-get install -y python3.6 python-pip wget graphviz golang \
  && pip install -r requirements.txt

RUN set -ex \
  && apt-get install -y ruby ruby-dev \
  && gem install apiaryio

RUN set -ex \
  && apt-get install -y php-cli php-xml php-pear composer \
  && composer update
  #  && wget http://www.phpdoc.org/phpDocumentor.phar \
  #  && chmod +x /src/phpDocumentor.phar
  #  && pear channel-discover pear.phpdoc.org \
  #  && pear install phpdoc/phpDocumentor

RUN set -ex \
  && wget https://github.com/bukalapak/snowboard/releases/download/v1.1.0/snowboard-v1.1.0.linux-amd64.tar.gz \
  && tar xzf snowboard-v1.1.0.linux-amd64.tar.gz \
  && mv snowboard /usr/local/bin/ \
  && rm snowboard-v1.1.0.linux-amd64.tar.gz
