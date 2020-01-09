FROM alpinelab/ruby-dev

RUN apt-get update && apt-get install --assume-yes --no-install-recommends ruby-dev

WORKDIR /usr/src/app

COPY Gemfile Gemfile.lock ./
COPY app/ .
COPY app/peluqueriaiv.rb app/peluqueriaiv.rb
COPY src/ .
COPY src/cita.rb src/cita.rb
COPY datos/ .
COPY datos/datoscita.json datos/datoscita.json
COPY config.ru .
COPY heroku.yml .
COPY Procfile .
COPY rakefile .
COPY test.rb .

RUN bundle update

RUN bundle install

CMD ["bundle", "exec", "rackup", "-p", "80", "--host", "0.0.0.0"]
