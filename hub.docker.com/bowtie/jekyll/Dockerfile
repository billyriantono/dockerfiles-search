FROM ruby

ENV PORT "4000"
ENV HOST "0.0.0.0"

EXPOSE $PORT

RUN mkdir -p /app

WORKDIR /app

RUN gem install jekyll jekyll-paginate bundler

COPY ./docker-entrypoint.sh /

ENTRYPOINT [ "/docker-entrypoint.sh" ]

CMD [ "jekyll" ]
