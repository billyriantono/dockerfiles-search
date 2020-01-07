FROM python:2.7.14-alpine

LABEL author="Kan yun <849405952@gmail.com>"

RUN apk add --no-cache gcc musl-dev openssl-dev libffi-dev
COPY . /skeleton
WORKDIR /skeleton
RUN pip install -r requirements.txt
EXPOSE 5000
ENTRYPOINT ["sh", "scripts/dev.sh"]
