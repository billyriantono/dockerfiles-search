FROM bretfisher/jekyll-serve

RUN apk add --no-cache nodejs

CMD [ "bundle", "exec", "jekyll", "serve", "--force_polling", "--future", "-H", "0.0.0.0", "-P", "4000" ]
