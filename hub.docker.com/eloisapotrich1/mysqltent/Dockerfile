FROM mikesir87/aws-cli

RUN apk add --no-cache imagemagick git ruby ruby-bundler
RUN gem install --no-user-install --no-document iiif_s3
ADD script.sh /usr/local/bin/script.sh

ENTRYPOINT ["/usr/local/bin/script.sh"]
