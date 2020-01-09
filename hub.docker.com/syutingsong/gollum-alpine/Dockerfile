FROM ruby:alpine3.10
RUN echo "https://mirror.csclub.uwaterloo.ca/alpine/v3.10/main"\
   > /etc/apk/repositories && \
   echo "https://mirror.csclub.uwaterloo.ca/alpine/v3.10/community" \
   >>/etc/apk/repositories && \
   apk add --no-cache build-base cmake icu-dev icu-libs git && \
   gem install gollum github-markdown && \
   apk del cmake build-base icu-dev
WORKDIR /wiki
ENTRYPOINT ["/usr/local/bin/ruby", "/usr/local/bundle/bin/gollum"]
CMD ["--port", "8080", "--live-preview"]

