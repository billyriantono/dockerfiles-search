ARG codeversion="latest"
from ubuntu:$codeversion
run echo $codeversion
ARG license_key="1234-567"
ENV ora_port=1521
label maintainer hasmukh.babaria@oracle.com
run mkdir /code
copy sample.sh /code/sample.sh
run chmod +x /code/sample.sh
run echo $license_key
workdir /code
cmd sh /code/sample.sh 
