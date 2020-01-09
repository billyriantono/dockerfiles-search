FROM ruby
ENV PORT=9000
WORKDIR /app
COPY . /app
COPY ./entrypoint.sh /bin/entrypoint.sh
EXPOSE $PORT
ENTRYPOINT ["/bin/entrypoint.sh"]
