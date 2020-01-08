FROM python:alpine
LABEL maintainer="363635454@qq.com"
WORKDIR /app
COPY . .
RUN apk add --no-cache libstdc++ && \
    apk add --no-cache --virtual BUILD python3-dev build-base && \
    pip install --no-cache-dir -r requirements.txt && \
    apk del BUILD
EXPOSE 8888
CMD [ "python", "./etcdtool.py" ]