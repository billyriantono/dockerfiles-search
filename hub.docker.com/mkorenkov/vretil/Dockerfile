# TODO: protoc generation (does not generate services, most likely, plugin missing in znly/protoc)
# FROM znly/protoc as protoc
# COPY scribe /scribe
# RUN cd / && protoc -I scribe scribe/*.proto --go_out=plugins=grpc:scribe


FROM golang as builder
COPY . /myapp
# COPY --from=protoc /scribe/*.pb.go /myapp/scribe
RUN cd /myapp && go mod download
RUN cd /myapp && CGO_ENABLED=0 go build -o /bin/myapp apps/server/server.go
# Create a "nobody" non-root user for the next image by crafting an /etc/passwd
# file that the next image can copy in. This is necessary since the next image
# is based on scratch, which doesn't have adduser, cat, echo, or even sh.
RUN echo "nobody:x:65534:65534:Nobody:/:" > /etc_passwd

# myapp golang container
FROM scratch

COPY --from=builder /bin/myapp /myapp
COPY --from=builder /etc/ssl/certs/ca-certificates.crt /etc/ssl/certs/
COPY --from=builder /etc_passwd /etc/passwd

ENV MYAPP_LISTEN_ADDR=":8001"
ENV MYAPP_SERVICE_ID="myapp"

USER nobody
ENTRYPOINT ["/myapp"]
EXPOSE "8001/tcp"