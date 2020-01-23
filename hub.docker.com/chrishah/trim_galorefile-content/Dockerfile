FROM python:2-alpine
RUN apk add --no-cache --update rsync
RUN pip install Markdoc
COPY markdoc.cron /var/spool/cron/crontabs/root
WORKDIR /site
# Build and start cron to rebuild every so often
CMD markdoc build && crond -l 2 -f

