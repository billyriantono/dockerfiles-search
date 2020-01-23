ARG codeversion="latest"
from ubuntu:$codeversion
run echo $codeversion
ARG license_key="1234-789"
ENV ORA_PORT=1521
label maintainer abnreddy.a@gmail.com
run mkdir /code
copy Sample.sh /code/Sample.sh
run chmod +x /code/Sample.sh
run echo $license_key
workdir /code
cmd sh /code/Sample.sh
# cmd ["/bin/bash", "sh", "Sample.sh"]
