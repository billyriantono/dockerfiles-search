FROM nginx
WORKDIR /srv/acestream
ENV COLUMNS=116
ADD search.py .
COPY nginx.conf /etc/nginx
COPY default.conf /etc/nginx/conf.d
RUN apt-get update &&                                                                                  \
    apt-get install -y --no-install-recommends                                                         \
        libpython2.7 python-pkg-resources net-tools python-apsw curl unzip python-setuptools           \
        uwsgi-plugin-python python-flask python-lxml python-m2crypto htop;                             \
    curl http://acestream.org/downloads/linux/acestream_3.1.49_debian_9.9_x86_64.tar.gz |              \
    tar xzf -;                                                                                         \
    curl -kL https://github.com/vstavrinov/acestream_search/archive/master.zip > acestream_search.zip; \
    unzip acestream_search.zip;                                                                        \
    cd acestream_search-master;                                                                        \
    python setup.py install;                                                                           \
    cd -;                                                                                              \
    usermod -d /srv/acestream www-data;                                                                \
    chown -R www-data ./ /etc/nginx /var/cache/nginx;                                                  \
    apt-get clean;                                                                                     \
    apt autoremove -y;                                                                                 \
    rm --force --recursive /var/lib/apt/lists;                                                         \
    rm -rf ./data/plugins/*
USER www-data
CMD sed -i -e "s/PORT/$PORT/" -e "s/port/${port:=80}/" /etc/nginx/conf.d/default.conf;        \
    chmod 600 /etc/nginx/conf.d/default.conf;                                                 \
    ./acestreamengine --client-console --bind-all --live-cache-type memory --vod-cache-type memory --live-buffer 25 --vod-buffer 20 --vod-drop-max-age 120 --stats-report-interval 2 --stats-report-peers --service-remote-access --access-token 9999 --cache-dir /tmp/ --state-dir /tmp/ --log-file /tmp/log & \
    uwsgi_python -s 127.0.0.1:3031 --wsgi-file search.py --callable app -p 4 --threads 4 -M & \
    nginx -g "daemon off;"
