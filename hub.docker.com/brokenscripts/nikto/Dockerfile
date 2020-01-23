FROM alpine:edge
LABEL maintainer "Thomas"

RUN apk --update --no-cache add make \
                                perl \
                                perl-net-ssleay \
                                git \
    &&  git clone https://github.com/sullo/nikto.git \
    &&  apk del git \
    &&  rm -rf /nikto/.git

RUN adduser -D nikto \
  && chown -R nikto /nikto

USER nikto

ENV PATH /nikto/program:$PATH

WORKDIR /nikto/program

ENTRYPOINT ["nikto.pl"]
CMD [ "-Help"]
