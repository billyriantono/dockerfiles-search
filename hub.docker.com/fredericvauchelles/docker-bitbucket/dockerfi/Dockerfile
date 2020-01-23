FROM          python:2-alpine

MAINTAINER    FreakErn git@freakern.de

RUN           python -m pip install configparser && \
                  python -m pip install netaddr && \
                  apk add --no-cache build-base && \
                  python -m pip install pycryptodome && \
                  apk add --no-cache git

RUN           cd /tmp && git clone https://github.com/mjg59/python-broadlink.git pb && cd pb && git checkout dd0e9083172d1ee54eec167d342edb3b157aea4c && python setup.py install && cd ../ && rm -rf pb

RUN           cd / && git clone https://github.com/davorf/BlackBeanControl.git blackbeancontrol  && cd blackbeancontrol && chmod +x BlackBeanControl.py

WORKDIR       /blackbeancontrol
RUN           cd /blackbeancontrol && echo -e '#!/bin/sh\n\npython /blackbeancontrol/BlackBeanControl.py -c $@' > entrypoint.sh && chmod +x entrypoint.sh
ENTRYPOINT    ["/blackbeancontrol/entrypoint.sh"]
