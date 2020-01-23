FROM metabase/metabase:v0.29.3

RUN apk add --no-cache curl

RUN curl -L -o /usr/local/bin/param-inject https://github.com/rbi13/aws-param-inject/releases/download/0.0.2/aws-param-inject-linux-386 && \
   chmod +x /usr/local/bin/param-inject

ENTRYPOINT ["param-inject","/app/run_metabase.sh"]
