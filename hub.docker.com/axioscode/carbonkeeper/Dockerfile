FROM node:8-slim

# Install Git, do cleanup after to keep layer size small
RUN apt-get update && \
    apt-get install --no-install-recommends -y git && \
    apt-get clean

# Install Yarn latest from pubbed bins (with key verification)
RUN set -ex \
  && for key in \
    6A010C5166006599AA17F08146C2130DFD2497F5 \
  ; do \
    gpg --batch --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys "$key" || \
    gpg --batch --keyserver hkp://ipv4.pool.sks-keyservers.net --recv-keys "$key" || \
    gpg --batch --keyserver hkp://pgp.mit.edu:80 --recv-keys "$key" ; \
  done \
  && curl -fsSLO --compressed "https://yarnpkg.com/latest.tar.gz" \
  && curl -fsSLO --compressed "https://yarnpkg.com/latest.tar.gz.asc" \
  && gpg --batch --verify latest.tar.gz.asc latest.tar.gz \
  && rm -rf /opt/yarn* \
  && tar -xzf latest.tar.gz -C /opt/ \
  && ln -nsf /opt/yarn-v*/bin/yarn /usr/local/bin/yarn \
  && ln -nsf /opt/yarn-v*/bin/yarnpkg /usr/local/bin/yarnpkg \
  && rm latest.tar.gz.asc latest.tar.gz

RUN yarn global add greenkeeper-lockfile@2

ADD ./docker-entrypoint.sh /

ENTRYPOINT ["/docker-entrypoint.sh"]
