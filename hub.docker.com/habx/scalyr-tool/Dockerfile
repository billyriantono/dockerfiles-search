FROM python:3-alpine3.10

ADD https://raw.githubusercontent.com/scalyr/scalyr-tool/master/scalyr /bin/scalyr
RUN chmod u+x /bin/scalyr
ENTRYPOINT ["/bin/scalyr"]
