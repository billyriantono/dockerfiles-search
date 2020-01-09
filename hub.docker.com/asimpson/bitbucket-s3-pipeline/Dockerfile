FROM ruby:2.4.0

ENV LANG C.UTF-8

RUN gem install s3_website

RUN apt-get update
RUN apt-get install -y openjdk-7-jre-headless advancecomp gifsicle jhead jpegoptim libjpeg-progs optipng pngcrush pngquant

VOLUME ["/website", "/config"]

WORKDIR /website

ENTRYPOINT ["s3_website"]

CMD ["--help"]
