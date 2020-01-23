# docker run -p 5000:5000 -v /var/run/docker.sock:/var/run/docker.sock aloukinas/docker-api:latest
#
# When running this container you will need to pass through the docker.sock
#
#

FROM python:3-alpine

# maintainer
LABEL maintainer = "Anthony Loukinas <anthony.loukinas@redhat.com>"

RUN apk add git &&\
    git clone https://github.com/anthonyloukinas/docker-api.git &&\
    cd /docker-api &&\
    pip install -r requirements.txt &&\
    export FLASK_APP=/docker-api/client.py &&\
    apk del git &&\
    rm -rf /var/cache/apk/*

ENTRYPOINT [ "python" ]

CMD [ "/docker-api/client.py" ]
