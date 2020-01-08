FROM node:10-alpine as build_ui

COPY ./ui /ui
WORKDIR /ui
RUN npm install

ENV PUBLIC_URL=/greengrass
RUN npm run build

FROM python:3-alpine

COPY requirements.txt /
RUN pip3 install --no-cache-dir -r requirements.txt

WORKDIR /app
COPY . .
COPY --from=build_ui /ui/build ./ui/build

RUN apk add --update openssh-client sshpass && rm -rf /var/cache/apk/*

# Bind-mount to host for persistance with `--volume`.
ENV MAGIC_DIR=/app/.gg

# This tell boto3 to pick credentials from this file,
# and tells the app to put it there.
ENV AWS_SHARED_CREDENTIALS_FILE=/app/.gg/credentials

EXPOSE 8887

CMD ["python3", "-m", "service.app"]
