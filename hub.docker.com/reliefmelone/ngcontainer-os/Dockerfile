FROM angular/ngcontainer:latest

LABEL maintainer="Relief Melone"
LABEL repository="https://github.com/relief-melone/ngcontainer-os"

USER root

RUN chgrp -R root /home/circleci && \
    chmod -R 770 /home/circleci

ENV HOME /home/circleci

USER 1001

ENTRYPOINT ["/bin/bash", "--login"]
