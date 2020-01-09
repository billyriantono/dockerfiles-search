FROM python:3-alpine

VOLUME /opt/cloudfleet-blog/output
WORKDIR /opt/cloudfleet-blog

RUN pip install pelican Markdown

COPY . /opt/cloudfleet-blog

CMD pelican -drt cloudfleet-pelican-theme content
