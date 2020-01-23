FROM ruby
RUN apt-get -y update && apt-get -y install libicu-dev cmake && rm -rf /var/lib/apt/lists/*
RUN gem install github-linguist
RUN gem install gollum
RUN gem install org-ruby  # optional
RUN gem install gollum-rugged_adapter
WORKDIR /wiki
ENTRYPOINT ["gollum", "--port", "80", "--adapter", "rugged", "--allow-uploads", "page"]
EXPOSE 80
