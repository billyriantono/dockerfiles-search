FROM ruby
RUN apt-get -y update && apt-get -y install libicu-dev cmake && rm -rf /var/lib/apt/lists/*; \
    gem install github-linguist github-markdown gollum org-ruby
WORKDIR /srv
ENTRYPOINT ["gollum", "--port", "80"]
EXPOSE 80
