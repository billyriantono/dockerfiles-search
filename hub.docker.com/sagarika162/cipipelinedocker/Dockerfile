arg code_version="latest"
from ubuntu:$code_version
run echo $code_version
arg license_key="123-456"
env ora_port=1521
label maintainer sanangia
run mkdir /code
copy sample.sh /code/sample.sh
run chmod +x /code/sample.sh
run echo $license_key
workdir /code
cmd sh /code/sample.sh
