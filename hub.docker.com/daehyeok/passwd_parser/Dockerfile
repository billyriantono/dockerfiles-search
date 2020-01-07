FROM golang:1.11-alpine

RUN apk --no-cache add git

COPY . /passwd_parser

RUN cd  /passwd_parser && go install && rm -rf /passwd_parser

CMD ["passwd_parser", "-pretty"]
