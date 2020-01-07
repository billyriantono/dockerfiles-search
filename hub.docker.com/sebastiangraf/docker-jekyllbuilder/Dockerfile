FROM ruby:alpine
MAINTAINER Sebastian Graf <sg@toolsmith.ch>

RUN apk update \
  && apk add build-base 
  

RUN gem install \
  jekyll \
  jekyll-sitemap \
  jekyll-feed \
  jekyll-seo-tag \
  jekyll-paginate \
  jekyll-redirect-from
  

VOLUME /src
WORKDIR /src
ENTRYPOINT ["jekyll"]
CMD ["build"]