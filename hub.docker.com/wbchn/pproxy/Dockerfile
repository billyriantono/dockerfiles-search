#
# Docker for https://github.com/qwj/python-proxy, support socks/http/ss, and so on.
#
FROM python:3.6-alpine

MAINTAINER wbchn wbin.chn@gmail.com

RUN pip install pproxy

# user define from args, such as: -e "args=-i ss://aes-256-cfb:passwords@0.0.0.0:1888"
CMD pproxy ${args}
