FROM nginx:alpine

ADD entrypoint.sh /entrypoint.sh
RUN chmod a+x /entrypoint.sh
ENV HTML_CONTENT "Hello world! Change this content using the HTML_CONTENT environment variable"

ENTRYPOINT /entrypoint.sh