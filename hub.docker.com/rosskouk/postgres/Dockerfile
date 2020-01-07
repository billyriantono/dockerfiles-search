FROM postgres:12.0

# Set maintainer field
LABEL maintainer="automatr901 - automatr901@gmail.com"

# Set locale to en_GB as the default is en_US
RUN localedef -i en_GB -c -f UTF-8 -A /usr/share/locale/locale.alias en_GB.UTF-8
ENV LANG en_GB.utf8