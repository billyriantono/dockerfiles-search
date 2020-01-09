FROM alpine:3.8
RUN apk add --no-cache gcc musl-dev hiredis-dev make
WORKDIR /src
ADD . /src
RUN make

FROM alpine:latest
RUN apk --no-cache add ca-certificates
WORKDIR /root/
COPY --from=0 /src .
ENTRYPOINT ["./vulcan"]
