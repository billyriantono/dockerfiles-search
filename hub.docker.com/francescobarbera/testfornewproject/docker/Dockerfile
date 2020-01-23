FROM nginx:1.17

RUN apt-get update && apt-get install -y \
      git \
      && rm -rf /usr/share/doc/* && \
      rm -rf /usr/share/info/* && \
      rm -rf /tmp/* && \
      rm -rf /var/tmp/*
RUN rm -rf /usr/share/nginx/html/*
RUN git clone --depth 1 https://github.com/fr3nd/christmas-runner.git /usr/share/nginx/html
