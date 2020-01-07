# Dockerfile for Redis with Perl
# acdaic4v 21.08.2015
FROM acdaic4v/ubuntu-perl-base:v20161124
MAINTAINER acdaic4v <acdaic4v@sloervi.de>

# Perl Modules for Redis
RUN cpanm Redis
# Cleanup CPAN- Directory
RUN rm -rf .cpanm
