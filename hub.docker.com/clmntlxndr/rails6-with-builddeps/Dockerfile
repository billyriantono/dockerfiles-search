FROM clmntlxndr/ruby-over-node
RUN apk add --no-cache --virtual .gems-builddeps build-base linux-headers ruby-dev postgresql-dev sqlite-dev libxml2-dev libxslt-dev
RUN apk add --no-cache --virtual .usual-gems-rundeps tzdata imagemagick libpq sqlite-libs git
WORKDIR /app
COPY Gemfile /app
RUN bundle install

