ARG codeversion="latest"
FROM ubuntu:$codeversion
run echo $codeversion
ARG license_key="1234-789"
ENV ORA_PORT=1521
label maintainer rajesh.dronamraju@gmail.com
RUN mkdir /code
copy sample.sh /code/sample.sh
run chmod +x /code/sample.sh
run echo $license_key
workdir /code
cmd sh /code/sample.sh
