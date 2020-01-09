FROM alpine:3

RUN apk add --no-cache --virtual=nut-bootstrap \
    gcc musl-dev libffi-dev python3-dev openssl-dev zlib-dev jpeg-dev && \
    mkdir -p /app/nut && \
    wget -qO- http://tinfoil.io/repo/nut.src.latest.zip | unzip -d /app/nut - && \
    pip3 install --no-cache-dir colorama pyopenssl requests tqdm unidecode \
    Pillow BeautifulSoup4 urllib3 Flask google-api-python-client google-auth-oauthlib && \
    apk del --purge nut-bootstrap && \
    apk add --no-cache python3 libjpeg-turbo && \
    cat conf/nut.default.conf | sed -e 's/\"\.\"/\"\/games\"/g'

ENV PYTHONIOENCODING="UTF-8"

EXPOSE 9000
VOLUME /app/nut/conf/ games/

CMD ["python3", "/app/nut/nut.py", "-S"]