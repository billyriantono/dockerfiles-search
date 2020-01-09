arg code_version="latest"
FROM ubuntu:$code_version
LABEL MAINTAINER amaradevi@gmail.com
run echo $code_version
arg license_key="123-456"
env ora_port=1521
## vailable for containers
RUN mkdir /code
copy sample.sh /code/sample.sh
RUN chmod +x /code/sample.sh
run echo $license_key
WORKDIR /code
CMD sh /code/sample.sh
