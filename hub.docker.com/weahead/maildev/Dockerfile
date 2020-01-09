FROM weahead/nodejs:6.2.2

MAINTAINER We ahead <docker@weahead.se>

EXPOSE 3001

ENTRYPOINT ["/app/bin/maildev", "--web", "3000", "--smtp", "3001"]
