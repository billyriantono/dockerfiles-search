ARG codeversion="latest"
from ubuntu:$codeversion
RUN echo $codeversion
ARG License_key="1234-789"
ENV ORA_PORT=1521
label maintainer chaitanya.bodireddy@oracle.com
run mkdir /code
copy Sample.sh /code/Sample.sh
run chmod +x /code/Sample.sh
run echo $License_key
workdir /code
cmd sh /code/Sample.sh
#cmd
