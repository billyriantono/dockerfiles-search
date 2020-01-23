arg code_version="latest"
from ubuntu:$code_version
run echo $code_version
arg license_key="123-456"
env ora_port=1521
label maintainer ankur34984@gmail.com
run apt-get -y update
run apt-get -y install curl apache2
copy boot.sh /etc/boot.sh
RUN chmod +x /etc/boot.sh
run echo $license_key
WORKDIR /code
CMD apachectl -D FOREGROUND
