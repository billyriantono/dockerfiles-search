# Dockerfile extending the generic Node image with application files for a
# single application.
#FROM gcr.io/google_appengine/nodejs
#20180704 alpine does not come with apt-get. need to update this file to get it to work
FROM registry.ap-northeast-1.aliyuncs.com/kaituanxue/rendertron_base:1.0.0

COPY . /app/
#ADD thirdfonts /usr/share/fonts/thirdfonts
RUN fc-cache -fv

# Add botrender as a user
RUN groupadd -r botrender && useradd -r -g botrender -G audio,video botrender \
  && mkdir -p /home/botrender && chown -R botrender:botrender /home/botrender \
  && chown -R botrender:botrender /app

# Run botrender non-privileged
USER botrender

EXPOSE 3000
WORKDIR /app

RUN npm install || \
  ((if [ -f npm-debug.log ]; then \
  cat npm-debug.log; \
  fi) && false)

RUN npm run build
ENTRYPOINT [ "npm" ]
CMD ["run", "start"]
