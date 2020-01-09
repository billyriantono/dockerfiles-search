FROM jekyll/builder:4 AS BUILDER
RUN mkdir /srv/wuc.me
RUN chown -R jekyll:jekyll /srv/wuc.me
WORKDIR /srv/wuc.me
COPY --chown=jekyll:jekyll . .
RUN jekyll build

FROM nginx
EXPOSE 80
COPY --from=BUILDER /srv/wuc.me/_site /usr/share/nginx/html

