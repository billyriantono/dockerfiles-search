FROM mrt2016/ruby:2.3

RUN echo "source 'https://rubygems.org'" > Gemfile \
        && echo "gem 'rails', '4.2.5.1'" >> Gemfile \
        && bundle install \
        && rm Gemfile Gemfile.lock

CMD [ "rails s" ]
