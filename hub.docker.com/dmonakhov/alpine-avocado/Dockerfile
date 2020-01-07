FROM python:alpine

COPY requirements.txt /tmp/avocado-packets.txt
COPY xunit_mod_property /usr/bin/xunit_mod_property

RUN pip install -r /tmp/avocado-packets.txt && unlink /tmp/avocado-packets.txt
