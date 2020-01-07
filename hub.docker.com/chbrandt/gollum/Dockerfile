FROM ruby
RUN apt-get -y update && \
    apt-get -y install libicu-dev python-pip && \
    apt-get clean
RUN pip install docutils
RUN gem install gollum
RUN gem install redcarpet org-ruby
VOLUME /wiki
WORKDIR /wiki
CMD ["gollum", "--port", "80", "--mathjax"]
EXPOSE 80
