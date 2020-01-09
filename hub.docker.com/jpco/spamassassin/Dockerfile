FROM resin/armv7hf-debian-qemu
# Install package here for cache 
COPY assets/bin/*.sh /usr/local/bin/
RUN ["cross-build-start"]
RUN chmod +x /usr/local/bin/*.sh \
 && apt update \
 && apt -y install --no-install-recommends \
 spamassassin spamc \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/* \
  	/tmp/* \
  	/var/tmp/* \
 && sed -i 's/CRON=0/CRON=1/g; s/OPTIONS="/OPTIONS="--ip-address -p 6783 /g' /etc/default/spamassassin \
 && sed -i 's/# rewrite_header/rewrite_header/g; s/# required_score/required_score/g; s/# use_bayes/use_bayes/g; s/# bayes_auto_learn/bayes_auto_learn/g'  /etc/spamassassin/local.cf
RUN ["cross-build-end"]

ENV PORT=6783

USER debian-spamd
CMD run-sa.sh
