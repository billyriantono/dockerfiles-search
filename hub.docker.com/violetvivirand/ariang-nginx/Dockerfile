FROM nginx:alpine

RUN apk add --no-cache git curl jq unzip && \
  export version=$(curl --silent "https://api.github.com/repos/mayswind/AriaNg/releases/latest" | jq -r ".tag_name") && \
  wget https://github.com/mayswind/AriaNg/releases/download/$version/AriaNg-$version.zip && \
  unzip -o AriaNg-$version.zip -d /usr/share/nginx/html && \
  rm AriaNg-$version.zip
