# docker image for playing zork via webapp
# License: GPL
# (c) GreekSailor 2019
FROM python:3.7-alpine

RUN adduser -Ds /bin/sh flathead

USER flathead
RUN mkdir -p /home/flathead/gue/cgi-bin
WORKDIR /home/flathead/gue

COPY --chown=flathead:flathead dfrotz .
COPY --chown=flathead:flathead zork1.z3 .
COPY --chown=flathead:flathead index.html .
COPY --chown=flathead:flathead cgi-bin/zorkit cgi-bin/zorkit

RUN chmod a+x cgi-bin/zorkit
RUN ls -lR .

EXPOSE 8000
CMD ["python", "-m", "http.server", "--cgi"]
