FROM ruby:2.5-alpine

RUN apk add --no-cache build-base gcc bash cmake nodejs

RUN gem install bundler jekyll github-pages

EXPOSE 4000

WORKDIR /site

# create new site by setting -e JEKYLL_NEW=true
ENV JEKYLL_NEW false

COPY docker-entrypoint.sh /usr/local/bin/
RUN chmod +x /usr/local/bin/docker-entrypoint.sh
WORKDIR /site
ENTRYPOINT [ "docker-entrypoint.sh" ]
CMD [ "bundle", "exec", "jekyll", "serve", "--force_polling", "-H", "0.0.0.0", "-P", "4000" ]