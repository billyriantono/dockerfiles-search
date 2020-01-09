FROM docker:17.06.0-ce

RUN apk add --no-cache bash make curl python py-pip lua5.2 git

RUN pip install docker-compose awscli

RUN ln -s /usr/bin/lua5.2 /usr/bin/lua

CMD [ "bash" ]

