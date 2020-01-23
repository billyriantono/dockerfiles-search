FROM golang as builder

RUN touch /var/log/access.log

RUN mkdir -p $GOPATH/src/github.com/cyberious/ltop
WORKDIR $GOPATH/src/github.com/cyberious/ltop
COPY . .
RUN chown root startup.sh
RUN chmod 755 startup.sh
RUN make deps

## Entrypoint has to be this way as TTY does not problem from the binary
ENTRYPOINT ["./startup.sh"]