FROM golang:1.8.3

RUN go get github.com/homecu/oauth2_proxy
COPY templates /templates
EXPOSE 80
ENTRYPOINT [ \
    "oauth2_proxy", \
    "-upstream=file:///dev/null", \
    "-custom-templates-dir=/templates", \
    "-http-address=0.0.0.0:80", \
    "-request-logging=true" \
]
