FROM mhart/alpine-node

RUN apk add --update python make g++ git bash
ADD runner.sh /runner.sh
RUN chmod +x /runner.sh

ADD let-run.sh /let-run.sh
RUN chmod +x /let-run.sh

ADD let-run.sh /watch.sh
RUN chmod +x /watch.sh
