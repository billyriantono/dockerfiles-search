FROM ctwise/ruby

RUN gem install jekyll --no-document
RUN gem install therubyracer --no-document
RUN gem install RedCloth --no-document
RUN gem install pry --no-document
RUN gem install jekyll-sitemap --no-document
RUN gem install jekyll-paginate --no-document
RUN gem install jekyll-mentions --no-document
RUN gem install jemoji --no-document

ENTRYPOINT ["jekyll"]
