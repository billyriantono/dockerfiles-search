########################################
# create by :cxh-PC
# create time :2018-05-10 11:19:48.892338
########################################
FROM python:3.6-alpine3.6
COPY ./requirements.txt /var/requirements.txt
COPY . /var/sync_db2redis
RUN   echo http://dl-cdn.alpinelinux.org/alpine/v3.3/main > /etc/apk/repositories \
     && echo http://dl-cdn.alpinelinux.org/alpine/v3.3/community >> /etc/apk/repositories \
     && apk add --no-cache --virtual .build-deps  \
                freetds-dev \
     && echo http://dl-cdn.alpinelinux.org/alpine/v3.6/main > /etc/apk/repositories \
     && echo http://dl-cdn.alpinelinux.org/alpine/v3.6/community >> /etc/apk/repositories \
     && apk add --no-cache --virtual .build-deps  \
        make \
		gcc \
		libc-dev \
		linux-headers \
		python3-dev \
    && pip3 install -r /var/requirements.txt \
    && python /var/sync_db2redis/setup.py install \
    && find /var/sync_db2redis -depth \
		\( \
		    \( -type d -a -name app -o -name extras -o -name build -o -name .git -o -name .idea -o -name __pycache__ \) \
		    -o \
		    \( -type f -a -name '*.pyc' -o -name '*.pyo'  -o -name '*.c'\
		       -o -name 'README.md' -o -name 'run.sh'  -o -name 'run-dev.sh' \
		       -o -name 'setup.py' -o -name 'requirements.txt' -o -name 'Dockerfile' \
		       -o -name 'docker-compose-dev.yaml' \) \
		\) -exec rm -rf '{}' + \
	&& find /usr/local -depth \
		\( \
		    \( -type d -a -name test -o -name tests \) \
		    -o \
		    \( -type f -a -name '*.pyc' -o -name '*.pyo' \) \
		\) -exec rm -rf '{}' + \
	&& runDeps="$( \
		scanelf --needed --nobanner --recursive /usr/local \
			| awk '{ gsub(/,/, "\nso:", $2); print "so:" $2 }' \
			| sort -u \
			| xargs -r apk info --installed \
			| sort -u \
	)" \
	&& apk add --virtual .python-rundeps $runDeps \
    && apk del .build-deps
