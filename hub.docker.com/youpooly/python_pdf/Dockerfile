FROM python:3.5.2-slim

MAINTAINER Christopher Lege <christopher.lege@youpooly.com>

RUN apt-get update && apt-get -y install gcc make libssl-dev libffi-dev g++ ca-certificates libtool m4 libuv-dev automake autoconf libxml2 libxml2-dev libcairo2 libpango1.0-0 libgdk-pixbuf2.0-0 shared-mime-info \
    && pip3 install nose \
    && pip3 install certifi==14.5.14 easydict==1.6 enum34==1.1.2 motorengine==0.9.0 psutil==2.2.1 pyasn1==0.1.7 pycares==0.6.1 pycparser==2.10 python-dateutil==2.2 python-etcd==0.3.2 python-json-logger==0.1.1 python-logstash==0.4.5 pytz==2015.2 PyYAML==3.11 boto requests six==1.9.0 termcolor==1.1.0 tornado uvloop tornaduv ujson==1.33 weasyprint
   # && apk del gcc musl-dev linux-headers python3-dev make openssl-dev g++ python3-tests python3-doc openssl-dev openssl-doc make linux-headers g++ libc-dev musl-dev libc6-compat musl-dbg gcc mpc1 mpfr3 gmp libstdc++ libgcc
