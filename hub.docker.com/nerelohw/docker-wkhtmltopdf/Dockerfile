FROM nerelohw/alpine-wkhtmltopdf:3.8-0.12.5-small as builder

FROM nerelohw/docker-alpine:3.8

##ref:https://bitbucket.org/wholeren/docker-wkhtmltopdf-builder
##check Dockerfile-alpine.template

RUN apk add --no-cache \
  libstdc++ \
  libx11 \
  libxrender \
  libxext \
  libssl1.0 \
  ca-certificates \
  fontconfig \
  freetype \
  ttf-dejavu \
  ttf-droid \
  ttf-freefont \
  ttf-liberation \
  ttf-ubuntu-font-family

COPY --from=builder /bin/wkhtmltopdf /bin/wkhtmltopdf

#ENTRYPOINT ["wkhtmltopdf"]
##docker run nerelohw/docker-wkhtmltopdf google.com - > test.pdf
