FROM ruby:2.3.6-stretch

RUN set -ex; \
    useradd --create-home codewarrior; \
    ln -s /home/codewarrior /workspace;

# Use `~>` to avoid conflicts
RUN set -ex; \
    gem install \
# Authentication and OAuth
        bcrypt:'~> 3.1.11' \
        jwt:'~> 1.5.6' \
# API Builder and Discovery
        jbuilder:'~> 2.7.0' \
# Concurrency and Parallelism
        celluloid:'~> 0.17.3' \
        concurrent-ruby:'~> 1.0.5' \
        eventmachine:'~> 1.2.3' \
# Core Extensions
        activesupport:'~> 5.1.2' \
        hamster:'~> 3.0.0' \
        hashie:'~> 3.5.6' \
# Database Drivers
        pg:'~> 0.21.0' \
        mongo:'~> 2.4.3' \ 
        redis:'~> 3.3.3' \
        sqlite3:'~> 1.3.13' \
# Database Tools
        sequel:'~> 4.48.0' \
        connection_pool:'~> 2.2.1' \
# ORM/ODM
        mongoid:'~> 6.2.0' \
# Date and Time Processing
        chronic:'~> 0.10.2' \
# HTML/XML Parsing
        nokogiri:'~> 1.8.0' \
# HTTP Clients and tools
        faraday:'~> 0.12.2' \
        httparty:'~> 0.15.6' \
# Miscellaneous
        awesome_print:'~> 1.8.0' \
        concerning:'~> 1.1.0' \
        timers:'~> 4.1.2' \
# Testing: Extra
        timecop:'~> 0.9.1' \
# Testing: Fake Data
        faker:'~> 1.8.4' \
        factory_girl:'~> 4.8.0' \
# Testing: Frameworks
        rspec:'~> 3.6.0' \
        rspec-its:'~> 1.2.0' \
        rspec-rails:'~> 3.6.0' \
        capybara:'~> 2.14.4' \
# Testing: Mock
        webmock:'~> 3.0.1' \
        mock_redis:'~> 0.17.3' \
# Web Frameworks
        rails:'~> 5.1.2' \
        sinatra:'~> 2.0.0' \
# Web Servers
        rack:'~> 2.0.3' \
    ;

WORKDIR /workspace

COPY rootfs/runner /runner

USER codewarrior
ENV USER=codewarrior \
    HOME=/home/codewarrior
