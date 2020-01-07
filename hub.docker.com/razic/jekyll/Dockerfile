FROM ruby

RUN apt-get update -y  && \
    apt-get install -y \
    node \
    python-pygments && \
    gem install \
    github-pages \
    jekyll \
    jekyll-redirect-from \
    kramdown \
    rdiscount \
    rouge

EXPOSE 4000

ENTRYPOINT ["jekyll"]

CMD ["serve"]
