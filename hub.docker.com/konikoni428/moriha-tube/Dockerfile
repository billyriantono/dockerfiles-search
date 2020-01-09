FROM alpine:latest

RUN apk update && apk add -y \
    chromium \
    chromium-chromedriver \
    python3 \
    && pip3 install selenium requests
ENV TZ=Asia/Tokyo
COPY ./python /
CMD ["python3", "main.py", "&"]
