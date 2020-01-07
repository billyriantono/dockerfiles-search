FROM    jfloff/alpine-python:3.6 

MAINTAINER Robert Gusick "robert@gusick.com"

RUN     pip install \
                google-music-scripts

ENTRYPOINT ["/usr/bin/dumb-init", "/usr/local/bin/gms"]

CMD /bin/bash
