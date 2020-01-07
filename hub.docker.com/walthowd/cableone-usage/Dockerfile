FROM python:3
MAINTAINER Walt Howd <walthowd@gmail.com>

VOLUME ["/config"]

RUN mkdir -p /opt/cableone /config

COPY cableone/ /opt/cableone
RUN pip install --no-cache-dir -r /opt/cableone/requirements.txt

COPY . .

CMD [ "python", "/opt/cableone/cableone_usage.py" ]
