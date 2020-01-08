FROM golang:1.10 AS build
LABEL maintainer "Will McCutchen <will@mccutch.org>"
RUN go get github.com/mreiferson/ddstatsd

FROM gcr.io/distroless/base
COPY --from=build /go/bin/ddstatsd /bin/ddstatsd
EXPOSE 8126
ENTRYPOINT ["/bin/ddstatsd", "-config=/ddstatsd/rules.cfg"]
