FROM ruby:2.4

MAINTAINER david@codesmith.tech

RUN gem install \
	jekyll \
	jekyll-sitemap \
	jekyll-paginate \
	jekyll-gist

COPY ./jekyll-build.sh /jekyll-build.sh

CMD /jekyll-build.sh


