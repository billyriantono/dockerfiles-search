FROM bzohdy/java
MAINTAINER bzohdy
RUN echo "y"|/bin/bash -l -c 'sdk install gradle && sdk flush archives && sdk flush temp';
ENTRYPOINT /bin/bash
