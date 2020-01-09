FROM golang:latest
RUN mkdir -p /go/src/github.com/thegroundwork/awsbouncer
WORKDIR /go/src/github.com/thegroundwork/awsbouncer
COPY . /go/src/github.com/thegroundwork/awsbouncer

CMD ["go-wrapper", "run"]
RUN go-wrapper download
RUN go-wrapper install

RUN make getdeps
RUN make build
RUN make test
EXPOSE ${AWSBOUNCER_PORT:-6554}

# When running this container it will need AWS credentials.
# You can provide these from the host machine using something like the following
# docker run -p "6554:6554" -e "AWS_ACCESS_KEY_ID=$AWS_ACCESS_KEY_ID" -e "AWS_SECRET_ACCESS_KEY=$AWS_SECRET_ACCESS_KEY" awsbouncer

CMD ["bin/awsbouncer", "-aws-region=us-east-1"]
