FROM alfg/nginx-rtmp
WORKDIR /app
COPY requirements.txt /app
RUN apk add --no-cache --virtual=.run-deps python3 supervisor && \
    pip3 install --no-cache-dir --upgrade pip && \
    pip3 install --no-cache-dir -r requirements.txt

COPY . /app

COPY . /app

RUN set -x && cp config/nginx.conf /etc/nginx/nginx.conf && \
    cp config/supervisord.conf /etc/supervisord.conf && \
    cp config/supervisord.conf /etc/.original.supervisord.conf

ENV PYTHONUNBUFFERED=1 \
    PYTHONDONTWRITEBYTECODE=1

CMD ["/usr/bin/supervisord", "-n", "-c", "/etc/supervisord.conf"]