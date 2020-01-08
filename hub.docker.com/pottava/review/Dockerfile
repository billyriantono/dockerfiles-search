# Re:VIEW v3.1
#
# docker run --rm -v $(pwd):/doc pottava/review:3.1 review init mybook
# docker run --rm -v $(pwd)/mybook:/doc pottava/review:3.1 rake pdf
# docker run --rm -v $(pwd)/mybook:/doc -e REVIEW_CONFIG_FILE=config-ebook.yml pottava/review:3.1 rake epub

FROM pottava/latex:2019jp

RUN apk --no-cache add "ruby=2.5.3-r1"
RUN gem install --no-rdoc --no-ri review -v 3.1.0 \
    && rm -rf /usr/lib/ruby/gems/2.5.0/gems/rubyzip-1.2.2/test \
              /usr/lib/ruby/gems/2.5.0/gems/review-3.1.0/test \
              /usr/lib/ruby/gems/2.5.0/gems/rouge-3.3.0/lib/rouge/demos

RUN gem install --no-rdoc --no-ri rake -v 11.2.2

WORKDIR /doc
CMD ["review", "--help"]
