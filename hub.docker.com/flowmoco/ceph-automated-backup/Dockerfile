FROM rook/ceph:v0.9.2

RUN curl -O https://bootstrap.pypa.io/get-pip.py
RUN python get-pip.py
RUN rm -f get-pip.py
RUN pip install awscli --upgrade

ADD ./bin /usr/local/backupscripts


