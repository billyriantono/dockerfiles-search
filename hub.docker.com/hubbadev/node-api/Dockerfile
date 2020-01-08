FROM node:8-alpine

RUN \
  apk update && apk upgrade && apk add --no-cache curl bash\
  && INJ_RELEASE=$(curl -L -s -H 'Accept: application/json' https://github.com/rbi13/aws-param-inject/releases/latest)\
  && INJ_VERSION=$(echo $INJ_RELEASE | sed -e 's/.*"tag_name":"\([^"]*\)".*/\1/')\
  && curl -L -o /usr/local/bin/param-inject "https://github.com/rbi13/aws-param-inject/releases/download/$INJ_VERSION/aws-param-inject-linux-amd64"\
  && chmod +x /usr/local/bin/param-inject
