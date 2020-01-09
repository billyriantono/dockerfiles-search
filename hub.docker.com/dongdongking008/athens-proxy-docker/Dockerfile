FROM cuigh/athens-proxy
LABEL maintainer ="dongdongking008@163.com"

ADD proxy /usr/local/bin
RUN chmod +x /usr/local/bin/proxy
CMD ["proxy", "-config_file=/config/config.toml"]