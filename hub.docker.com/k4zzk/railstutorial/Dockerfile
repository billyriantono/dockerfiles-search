FROM rails:onbuild

ENV RAILS_ENV=production
ENV RAILS_SERVE_STATIC_FILES=true

RUN apt-get update \
    && apt-get install -y　\
      wget \
      curl \
      vim \
      imagemagick
    && rm -rf /var/lib/apt/lists/*

WORKDIR /usr/src/app

COPY . /usr/src/app
RUN bundle install

EXPOSE 3000
CMD ["./docker/app.sh"]
