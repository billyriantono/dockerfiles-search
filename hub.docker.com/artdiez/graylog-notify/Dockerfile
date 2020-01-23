FROM python:3
MAINTAINER Artem Kozlov <kozlov.artem@gmail.com>
RUN useradd -c 'Jarvis user' -m -d /home/jarvis -s /bin/bash jarvis \
    && mkdir -p /opt/graylog-notify/ \
    && chown -R jarvis:jarvis /opt/graylog-notify/ \
    && echo "Europe/Moscow" > /etc/timezone
WORKDIR /opt/graylog-notify/
COPY src/ /opt/graylog-notify/
RUN pip install -r requirements.txt
USER jarvis
EXPOSE 8080
CMD ["gunicorn", "--bind", " :8080", "--workers=2", "wsgi:app"]