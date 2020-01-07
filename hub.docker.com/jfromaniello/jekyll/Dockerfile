FROM ruby

WORKDIR /data

RUN gem install therubyracer jekyll
ENV PORT 5000

CMD jekyll serve --port $PORT