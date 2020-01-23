FROM python:alpine

COPY dodyndns.py /usr/local/bin/dodyndns
RUN chmod +x /usr/local/bin/dodyndns

COPY requirements.txt /var/tmp/
RUN pip install -r /var/tmp/requirements.txt

RUN echo '* * * * * dodyndns --hostname $(hostname)' | crontab -
CMD crond -f
