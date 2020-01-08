FROM ruby:2.6.5-buster

ENV VERSION="1.8.2"
RUN gem install bashcov --version ${VERSION} --no-format-exec
RUN adduser bashcov -D -h /app
ENV PS4="+%N:%i>"

WORKDIR /app

CMD ["bashcov", "--help"]
