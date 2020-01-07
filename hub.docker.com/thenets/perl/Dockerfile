FROM perl:5.22

# secure by default ♥ (thanks to sri!)
ENV PERL_CPANM_OPT --verbose --mirror https://cpan.metacpan.org --mirror-only
RUN cpanm Digest::SHA Module::Signature && rm -rf ~/.cpanm
ENV PERL_CPANM_OPT $PERL_CPANM_OPT --verify

# reinstall cpanm itself, for good measure
RUN cpanm App::cpanminus && rm -rf ~/.cpanm

# System libs
RUN apt-get update && \
    apt-get install -y libmojolicious-perl \
        libdatetime-perl \
        libdatetime-format-iso8601-perl \
        libdatetime-format-pg-perl \
        libjson-maybexs-perl \
        libssl-dev  \
        libcompress-raw-lzma-perl \
        libio-compress-lzma-perl \
        libarchive-extract-perl \
        libpq-dev \
        libgif-dev

# Install CPANM libs
RUN set -x \
    && cpanm \
        Mojolicious \
        EV \
        DateTime \
        DateTime::Format::ISO8601 \
        DateTime::Format::Pg \
        JSON::MaybeXS \
        Moose \
        Types::Standard \
        File::BOM \
        Crypt::OpenSSL::AES \
        DBIx::Connector \
        Imager::QRCode \
        Crypt::CBC \
        IO::Compress::Lzma \
        Crypt::PBKDF2 \
        Authen::OATH \
        Convert::Base32 \
        File::Slurper \
        Net::Amazon::DynamoDB \
        Mojolicious::Plugin::ClientIP \
        DBD::Pg \
        Proc::PID::File \
        Imager::File::GIF \
        Chart::Clicker \
    && rm -rf ~/.cpanm
