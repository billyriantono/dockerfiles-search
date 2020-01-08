FROM unocha/alpine-base-s6-python3:latest

COPY app.py config.py gunicorn.py hxl_run /srv/config/

        # git \
RUN apk add --update --no-cache \
        sqlite && \
    mkdir -p \
        /etc/services.d/hxl \
        /srv/db \
        /srv/config \
        /srv/cache \
        /srv/output \
        /var/log/proxy && \
    curl -so /srv/config/config.py.TEMPLATE \
        https://raw.githubusercontent.com/HXLStandard/hxl-proxy/master/config.py.TEMPLATE && \
    curl -so /srv/config/schema.sql \
        https://raw.githubusercontent.com/HXLStandard/hxl-proxy/master/hxl_proxy/schema.sql && \
    sqlite3 /srv/db/hxl-proxy.db < /srv/config/schema.sql && \
    pip3 install --upgrade \
        pip && \
    pip3 install --upgrade \
        hxl-proxy==1.3 \
        gunicorn \
        requests-cache && \
    mv /srv/config/hxl_run /etc/services.d/hxl/run && \
    # cleanup \
    rm -rf /root/.cache && \
    rm -rf /var/lib/apk/*

    # apk del git && \

EXPOSE 5000

VOLUME ["/srv/db" "/srv/cache" "/srv/config" "/srv/output" "/var/log/proxy"]


#ARG HXL_PROXY_BRANCH

#ENV HXL_PROXY_BRANCH=${HXL_PROXY_BRANCH:-master}

#VOLUME ["/srv/db" "/srv/cache" "/srv/config" "/srv/output" "/srv/www" /var/log/proxy"]

    #    /srv/www \

    #git clone --depth 1 --branch ${HXL_PROXY_BRANCH} \
    #    https://github.com/HXLStandard/hxl-proxy.git /srv/www && \
    #pip install -r /srv/www/requirements.txt && \
    #sqlite3 /srv/db/hxl-proxy.db < /srv/www/hxl_proxy/schema.sql && \
    # just for this test \
    #pip uninstall -y libhxl && \
    #mkdir -p /srv/libhxl && \
    #cd /srv/libhxl && \
    #git clone --depth 1 --branch ${HXL_PROXY_BRANCH} https://github.com/HXLStandard/libhxl-python.git . && \
        #python3 setup.py install && \
    #rm -rf /srv/libhxl && \
