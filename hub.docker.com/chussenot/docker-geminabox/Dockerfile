FROM ruby:2.3-onbuild
RUN mkdir -p /geminabox/data
VOLUME ["/geminabox/data"]
EXPOSE 9292
CMD ["rackup", "--host", "0.0.0.0"]
