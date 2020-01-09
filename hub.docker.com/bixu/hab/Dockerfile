FROM alpine

RUN apk update \
  && apk add --no-cache "bash" "curl" \
  && adduser -S "hab" \
  && addgroup -S "hab" \
  && curl --silent https://raw.githubusercontent.com/habitat-sh/habitat/master/components/hab/install.sh | bash \
  && export HAB_LICENSE="accept" \
  && hab pkg install "core/hab-launcher" \
  && hab pkg install "core/hab-sup" \
  && apk del --no-cache "bash" "curl"
