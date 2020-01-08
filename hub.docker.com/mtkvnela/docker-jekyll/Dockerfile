FROM jekyll/minimal


RUN apk add --no-cache make build-base \
    && gem install --pre sprockets  \
    && gem install activesupport execjs nokogiri fastimage liquid-tag-parser jekyll-sanity pathutil extras sassc \
    && gem install rspec uglifier mini_racer image_optim image_optim_pack font-awesome-sass luna-rspec-formatters \
    && gem install autoprefixer-rails babel-transpiler mini_magick simplecov bootstrap crass rubocop rake pry \
    && gem install uglifier jekyll-gzip jekyll-minifier
