FROM bzohdy/java
MAINTAINER bzohdy
RUN echo "y"|/bin/bash -l -c 'sdk install maven && sdk flush archives && sdk flush temp';
ENTRYPOINT /bin/bash
