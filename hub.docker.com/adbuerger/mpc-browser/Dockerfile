FROM python:3-alpine3.6

RUN apk add --no-cache --virtual .build-deps g++ && \
    pip --no-cache-dir install numpy plotly dash pymongo && \
    apk del --no-cache .build-deps && \
    rm -rf /var/cache/apk/*

COPY ./browser/ /opt/

EXPOSE 5000

CMD ["python", "/opt/browser.py"]
