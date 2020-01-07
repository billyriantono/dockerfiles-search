FROM mimba/python-ml:0.0.8

# Grab requirements.txt.
ADD requirements.txt /tmp/requirements.txt

RUN pip install -qr /tmp/requirements.txt && \
    yum clean all && rm -rf /tmp/* /var/tmp/*