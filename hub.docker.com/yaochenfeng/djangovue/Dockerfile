FROM node:alpine as appfront
WORKDIR /usr/src/app
COPY . .
RUN npm install && npm run build


FROM python:3
ENV PYTHONUNBUFFERED 1
#RUN echo http://mirrors.aliyun.com/alpine/v3.6/main > /etc/apk/repositories; \
#    apk --update add --no-cache tzdata openssl-dev libffi-dev \
#    python-dev \
#    zlib-dev \
#    musl-dev \
#    libc-dev \
#    gcc \
#    mysql-client \
#    && pip install --upgrade pip
ENV TZ=Asia/Shanghai
WORKDIR /usr/src/app
COPY --from=appfront /usr/src/app .

RUN  pip install --no-cache-dir -r requirements.txt -i http://mirrors.aliyun.com/pypi/simple/ --trusted-host mirrors.aliyun.com


EXPOSE 8000
CMD ["python3", "manage.py", "runserver", "0.0.0.0:8000"]