FROM aleraru/bionic-php7.2-v8js:latest
MAINTAINER Pavel Pavlov <pavel.pavlov@alera.ru>
RUN export DEBIAN_FRONTEND=noninteractive && apt-get update && \
apt-get install -y apt-utils curl gnupg nginx && \
curl -sL https://deb.nodesource.com/setup_11.x | bash - && apt-get install -y nodejs && \
curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - && \
echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list && \
apt-get update && apt-get install -y yarn && \
apt-get remove -y apt-utils curl gnupg && \
apt-get autoremove -y && apt-get autoclean -y && apt-get clean -y && rm -rf /var/lib/apt/lists/* && \
rm -rf /root/.vpython-root/ && rm -rf /root/.vpython_cipd_cache/

ADD ./etc/nginx/sites-available/default /etc/nginx/sites-available/

CMD service php7.2-fpm start && nginx -g 'daemon off;'
