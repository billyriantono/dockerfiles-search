FROM docker:stable-git

RUN apk add --no-cache build-base curl python3 python3-dev zlib-dev jpeg-dev protobuf protobuf-dev openssl libffi-dev openssl-dev tzdata

RUN if [ ! -e /usr/bin/pip ]; then ln -sf `which pip3` /usr/bin/pip ; fi
RUN if [[ ! -e /usr/bin/python ]]; then ln -sf `which python3` /usr/bin/python; fi

RUN ln -fs /usr/share/zoneinfo/Etc/UTC /etc/localtime
RUN echo "Etc/UTC" >  /etc/timezone

RUN pip3 install docker-compose
