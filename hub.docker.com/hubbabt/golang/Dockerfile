FROM golang

RUN curl -L -o /usr/local/bin/param-inject https://github.com/rbi13/aws-param-inject/releases/download/0.0.2/aws-param-inject-linux-386 && \
    chmod +x /usr/local/bin/param-inject


ENTRYPOINT ["param-inject"]
