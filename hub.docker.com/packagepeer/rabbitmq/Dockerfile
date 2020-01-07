FROM rabbitmq:3.5
MAINTAINER Javier Jerónimo <jjeronimo@packagepeer.com>

# ################################################################################ Entry point
ADD pkgp-run.sh /pkgp-run.sh
RUN chmod u+x /pkgp-run.sh

EXPOSE 5672
EXPOSE 4369
EXPOSE 25672

# ################################################################################ Entry point
CMD ["/pkgp-run.sh"]
