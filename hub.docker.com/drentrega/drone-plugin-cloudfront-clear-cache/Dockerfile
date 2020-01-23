FROM drentrega/aws-cli:latest

LABEL vendor="Dr.Entrega" \
      maintainer="Dr.Entrega <technology+docker@drentrega.com>" \
      image="drentrega/aws-cli" \
      tag="latest"

ENV PLUGIN_DISTRIBUTION="secret" \
    PLUGIN_PATTERN="/*"

CMD ["sh", "-c", "aws cloudfront create-invalidation --distribution-id $(if [ ! -z \"${AWS_CLOUDFRONT_DISTRIBUTION_ID}\" ]; then echo $AWS_CLOUDFRONT_DISTRIBUTION_ID; else echo $PLUGIN_DISTRIBUTION; fi) --paths \"$PLUGIN_PATTERN\""]

# This dockerfile was auto-generated at 2019-04-16T19:00:23-03:00.

# In case of security branches, please contact technology+security@drentrega.com.