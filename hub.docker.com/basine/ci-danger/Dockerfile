FROM norionomura/swiftlint:latest

RUN swiftlint version

RUN apt-get update && apt-get install -y ruby ruby-dev
RUN ruby --version
RUN which ruby
RUN gem install bundler rake danger danger-swiftlint danger-xcov
RUN danger --version

CMD ["swiftlint", "lint"]
