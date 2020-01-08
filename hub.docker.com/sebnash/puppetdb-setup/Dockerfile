FROM sebnash/puppet-base
MAINTAINER Sebastian Nash <mail@sebnash.com>

ONBUILD RUN apt-get update && apt-get install -y puppet
ONBUILD RUN puppet agent --test --server $PUPPETSERVER --waitforcert 20
