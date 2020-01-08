FROM tklx/base:0.1.1
RUN apt-get update \
    && apt-get --no-install-recommends -y install php5-cli\
    && apt-clean --aggressive
CMD ["php","-v"]
