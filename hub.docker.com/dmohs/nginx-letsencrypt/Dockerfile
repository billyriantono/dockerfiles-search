FROM nginx

RUN true \
  && apt-get update \
  && apt-get install -y curl \
  && cd /opt \
  && curl -L https://github.com/letsencrypt/letsencrypt/archive/v0.5.0.tar.gz > letsencrypt.tar.gz \
  && apt-get clean \
  && tar -xf letsencrypt.tar.gz \
  && rm letsencrypt.tar.gz

# This command will actually install the tool.
RUN true \
  && cd /opt/certbot-* \
  && ./letsencrypt-auto --help \
  && apt-get clean \

COPY src/container/default.conf /etc/nginx/conf.d
