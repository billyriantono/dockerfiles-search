FROM xenocider/container:python3.7.3
LABEL maintainer="xenos <xenos.lu@gmail.com>"

COPY . /server

RUN pip3 install -r /server/requirements.txt -i http://pypi.douban.com/simple --trusted-host pypi.douban.com &&\
    rm -rf /root/.cache

RUN test -e /server/local && exit ||\
    apk add --no-cache --virtual .fetch-deps \
            nodejs \
            yarn &&\
    cd /server/frontend &&\
    yarn install &&\
    yarn build &&\
    cp -r dist/* /server/ &&\
    rm -rf /server/frontend &&\
    apk del .fetch-deps

ENV GITHUB_CLIENT_ID ""
ENV GITHUB_CLIENT_SECRET ""
VOLUME /server/config
EXPOSE 8888
CMD ["/usr/bin/python3", "/server/server.py"]
