FROM ruby:2.2.3-slim
MAINTAINER hoshinotsuyoshi<guitarpopnot330+docker@gmail.com>
RUN gem install aws-sdk --no-document -v 2.1.23
ENTRYPOINT ["ruby", "-raws-sdk", "-rpp", "-ropen-uri", "-e"]
CMD ["STDERR.puts %(USAGE:\ndocker run --rm hoshinotsuyoshi/ruby-aws-sdk [rubyscript here]); exit 1"]
