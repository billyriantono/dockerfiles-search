FROM euskadi31/gentoo-php:latest

RUN echo "dev-php/pecl-uuid ~amd64" >> /etc/portage/package.keywords
RUN echo "dev-php/pecl-redis ~amd64" >> /etc/portage/package.keywords
RUN echo "dev-php/pecl-imagick ~amd64" >> /etc/portage/package.keywords
RUN echo "dev-php/twig ~amd64" >> /etc/portage/package.keywords
RUN echo "dev-php/pecl-geoip ~amd64" >> /etc/portage/package.keywords
RUN echo "dev-php/pecl-apcu ~amd64" >> /etc/portage/package.keywords
RUN echo "media-gfx/imagemagick jpeg" >> /etc/portage/package.use

RUN emerge --jobs 4 dev-php/pecl-redis dev-php/pecl-imagick dev-php/pecl-geoip dev-php/pecl-apcu dev-php/pecl-uuid
