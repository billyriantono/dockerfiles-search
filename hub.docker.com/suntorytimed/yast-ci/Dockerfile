FROM yastdevel/ruby:sle15-sp1

RUN RUBY_VERSION=ruby`rpm --eval '%{rb_ver}' | cut -d '.' -f 1,2` && \
  zypper --non-interactive in --no-recommends --force-resolution -fy \
  kmod \
  xdg-utils \
  yast2-ntp-client \
  yast2-cluster \
  ShellCheck \
  perl-XML-XPath \
  "$RUBY_VERSION-rubygem-nokogiri" \
  && zypper clean -a \
  && rm -rf /usr/share/doc/

WORKDIR /usr/src/app

# just some smoke tests, make sure rake and YaST work properly,
# ensure there is no leftover in the working directory
RUN rake -r yast/rake -V && TERM=xterm yast2 proxy summary && \
  rm -rf /var/log/YaST2/y2log && rm -rf /usr/src/app/*
