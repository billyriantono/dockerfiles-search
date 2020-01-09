
FROM linkerlab/awstats

# get reports from mail.log
RUN chmod +x /awstats-7.3/tools/maillogconvert.pl

COPY ./awstats.linoxide.conf /usr/lib/cgi-bin/awstats/awstats.linoxide.conf

