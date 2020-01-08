FROM ruby:2.4.1-alpine

RUN gem install github_changelog_generator

VOLUME ["/app"]
WORKDIR /app

CMD ["--help"]
ENTRYPOINT ["github_changelog_generator"]
