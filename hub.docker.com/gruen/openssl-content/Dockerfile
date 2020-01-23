FROM ubuntu:latest

RUN apt update && apt upgrade -y && DEBIAN_FRONTEND=noninteractive apt install -y apache2 php php-mysql vim

#On met les config dans les dossier des sites disponnible
COPY www/www.wt18.ephec-ti.be.conf /etc/apache2/sites-available
COPY b2b/b2b.wt18.ephec-ti.be.conf /etc/apache2/sites-available
COPY intranet/intranet.wt18.ephec-ti.be.conf /etc/apache2/sites-available

#On créé un lien logic entre les config et le dossier sites-enabled
RUN ln -s /etc/apache2/sites-available/www.wt18.ephec-ti.be.conf /etc/apache2/sites-enabled
RUN ln -s /etc/apache2/sites-available/b2b.wt18.ephec-ti.be.conf /etc/apache2/sites-enabled
RUN ln -s /etc/apache2/sites-available/intranet.wt18.ephec-ti.be.conf /etc/apache2/sites-enabled

#On créé le dossier source racine pour notre site
RUN mkdir /var/www/www.wt18.ephec-ti.be

RUN mkdir /var/www/www.wt18.ephec-ti.be/css
RUN mkdir /var/www/www.wt18.ephec-ti.be/css/effects

RUN mkdir /var/www/www.wt18.ephec-ti.be/fonts

RUN mkdir /var/www/www.wt18.ephec-ti.be/images
RUN mkdir /var/www/www.wt18.ephec-ti.be/images/about-images
RUN mkdir /var/www/www.wt18.ephec-ti.be/images/blog-images
RUN mkdir /var/www/www.wt18.ephec-ti.be/images/home-images
RUN mkdir /var/www/www.wt18.ephec-ti.be/images/work

RUN mkdir /var/www/www.wt18.ephec-ti.be/js
RUN mkdir /var/www/www.wt18.ephec-ti.be/js/effects

RUN mkdir /var/www/www.wt18.ephec-ti.be/php

RUN mkdir /var/www/b2b.wt18.ephec-ti.be
RUN mkdir /var/www/b2b.wt18.ephec-ti.be/images
RUN mkdir /var/www/b2b.wt18.ephec-ti.be/images/about-images
RUN mkdir /var/www/b2b.wt18.ephec-ti.be/css
RUN mkdir /var/www/b2b.wt18.ephec-ti.be/css/effects
RUN mkdir /var/www/b2b.wt18.ephec-ti.be/js
RUN mkdir /var/www/b2b.wt18.ephec-ti.be/js/effects

RUN mkdir /var/www/intranet.wt18.ephec-ti.be
RUN mkdir /var/www/intranet.wt18.ephec-ti.be/css
RUN mkdir /var/www/intranet.wt18.ephec-ti.be/images
RUN mkdir /var/www/intranet.wt18.ephec-ti.be/images/blog-images

#Copie le fichier html dans le fichier source racine
COPY www/site/index.html /var/www/www.wt18.ephec-ti.be/index.html
COPY www/site/contact.html /var/www/www.wt18.ephec-ti.be/contact.html
COPY www/site/works-details.html /var/www/www.wt18.ephec-ti.be/works-details.html

COPY www/site/css/effects/component.css /var/www/www.wt18.ephec-ti.be/css/effects
COPY www/site/css/effects/normalize.css /var/www/www.wt18.ephec-ti.be/css/effects
COPY www/site/css/effects/set2.css /var/www/www.wt18.ephec-ti.be/css/effects

COPY www/site/css/bootstrap.min.css /var/www/www.wt18.ephec-ti.be/css
COPY www/site/css/font-awesome.min.css /var/www/www.wt18.ephec-ti.be/css
COPY www/site/css/responsive.css /var/www/www.wt18.ephec-ti.be/css
COPY www/site/css/style.css /var/www/www.wt18.ephec-ti.be/css

COPY www/site/images/about-images/about-image-1.jpg /var/www/www.wt18.ephec-ti.be/images/about-images
COPY www/site/images/about-images/about-image-2.jpg /var/www/www.wt18.ephec-ti.be/images/about-images
COPY www/site/images/about-images/about-image-3.jpg /var/www/www.wt18.ephec-ti.be/images/about-images

COPY www/site/images/home-images/image-1.jpg /var/www/www.wt18.ephec-ti.be/images/home-images
COPY www/site/images/home-images/image-2.jpg /var/www/www.wt18.ephec-ti.be/images/home-images
COPY www/site/images/home-images/image-3.jpg /var/www/www.wt18.ephec-ti.be/images/home-images
COPY www/site/images/home-images/image-4.jpg /var/www/www.wt18.ephec-ti.be/images/home-images
COPY www/site/images/home-images/image-5.jpg /var/www/www.wt18.ephec-ti.be/images/home-images
COPY www/site/images/home-images/image-6.jpg /var/www/www.wt18.ephec-ti.be/images/home-images
COPY www/site/images/home-images/image-7.jpg /var/www/www.wt18.ephec-ti.be/images/home-images
COPY www/site/images/home-images/image-8.jpg /var/www/www.wt18.ephec-ti.be/images/home-images
COPY www/site/images/home-images/image-9.jpg /var/www/www.wt18.ephec-ti.be/images/home-images

COPY www/site/images/work/works-image-1.jpg /var/www/www.wt18.ephec-ti.be/images/work
COPY www/site/images/work/works-image-2.jpg /var/www/www.wt18.ephec-ti.be/images/work
COPY www/site/images/work/works-image-3.jpg /var/www/www.wt18.ephec-ti.be/images/work

COPY www/site/images/favicon.ico /var/www/www.wt18.ephec-ti.be/images
COPY www/site/images/logo.png /var/www/www.wt18.ephec-ti.be/images

COPY www/site/js/effects/AnimOnScroll.js /var/www/www.wt18.ephec-ti.be/js/effects
COPY www/site/js/effects/classie.js /var/www/www.wt18.ephec-ti.be/js/effects
COPY www/site/js/effects/imagesloaded.js /var/www/www.wt18.ephec-ti.be/js/effects
COPY www/site/js/effects/masonry.pkgd.min.js /var/www/www.wt18.ephec-ti.be/js/effects
COPY www/site/js/effects/modernizr.custom.js /var/www/www.wt18.ephec-ti.be/js/effects

COPY www/site/fonts/FontAwesome.otf /var/www/www.wt18.ephec-ti.be/fonts
COPY www/site/fonts/fontawesome-webfont.eot /var/www/www.wt18.ephec-ti.be/fonts
COPY www/site/fonts/fontawesome-webfont.svg /var/www/www.wt18.ephec-ti.be/fonts
COPY www/site/fonts/fontawesome-webfont.ttf /var/www/www.wt18.ephec-ti.be/fonts
COPY www/site/fonts/fontawesome-webfont.woff /var/www/www.wt18.ephec-ti.be/fonts
COPY www/site/fonts/fontawesome-webfont.woff2 /var/www/www.wt18.ephec-ti.be/fonts
COPY www/site/fonts/glyphicons-halflings-regular.eot /var/www/www.wt18.ephec-ti.be/fonts
COPY www/site/fonts/glyphicons-halflings-regular.svg /var/www/www.wt18.ephec-ti.be/fonts
COPY www/site/fonts/glyphicons-halflings-regular.ttf /var/www/www.wt18.ephec-ti.be/fonts
COPY www/site/fonts/glyphicons-halflings-regular.woff /var/www/www.wt18.ephec-ti.be/fonts
COPY www/site/fonts/glyphicons-halflings-regular.woff2 /var/www/www.wt18.ephec-ti.be/fonts

COPY www/site/js/bootstrap.min.js /var/www/www.wt18.ephec-ti.be/js
COPY www/site/js/custom.js /var/www/www.wt18.ephec-ti.be/js
COPY www/site/js/html5shiv.js /var/www/www.wt18.ephec-ti.be/js
COPY www/site/js/jquery.contact.js /var/www/www.wt18.ephec-ti.be/js
COPY www/site/js/jquery.min.js /var/www/www.wt18.ephec-ti.be/js
COPY www/site/js/maps.js /var/www/www.wt18.ephec-ti.be/js
COPY www/site/js/nav.js /var/www/www.wt18.ephec-ti.be/js

COPY www/site/php/contactform.php /var/www/www.wt18.ephec-ti.be/php

COPY b2b/site/about.html /var/www/b2b.wt18.ephec-ti.be/index.html

COPY b2b/site/images/favicon.ico /var/www/b2b.wt18.ephec-ti.be/images
COPY b2b/site/images/logo.png /var/www/b2b.wt18.ephec-ti.be/images

COPY b2b/site/images/about-images/about-image-1.jpg /var/www/b2b.wt18.ephec-ti.be/images/about-images
COPY b2b/site/images/about-images/about-image-2.jpg /var/www/b2b.wt18.ephec-ti.be/images/about-images
COPY b2b/site/images/about-images/about-image-3.jpg /var/www/b2b.wt18.ephec-ti.be/images/about-images

COPY b2b/site/js/bootstrap.min.js /var/www/b2b.wt18.ephec-ti.be/js
COPY b2b/site/js/custom.js /var/www/b2b.wt18.ephec-ti.be/js
COPY b2b/site/js/html5shiv.js /var/www/b2b.wt18.ephec-ti.be/js
COPY b2b/site/js/jquery.contact.js /var/www/b2b.wt18.ephec-ti.be/js
COPY b2b/site/js/jquery.min.js /var/www/b2b.wt18.ephec-ti.be/js
COPY b2b/site/js/maps.js /var/www/b2b.wt18.ephec-ti.be/js
COPY b2b/site/js/nav.js /var/www/b2b.b2bwt18.ephec-ti.be/js

COPY b2b/site/js/effects/AnimOnScroll.js /var/www/b2b.wt18.ephec-ti.be/js/effects
COPY b2b/site/js/effects/classie.js /var/www/b2b.wt18.ephec-ti.be/js/effects
COPY b2b/site/js/effects/imagesloaded.js /var/www/b2b.wt18.ephec-ti.be/js/effects
COPY b2b/site/js/effects/masonry.pkgd.min.js /var/www/b2b.wt18.ephec-ti.be/js/effects
COPY b2b/site/js/effects/modernizr.custom.js /var/www/b2b.wt18.ephec-ti.be/js/effects

COPY b2b/site/css/effects/component.css /var/www/b2b.wt18.ephec-ti.be/css/effects
COPY b2b/site/css/effects/normalize.css /var/www/b2b.wt18.ephec-ti.be/css/effects
COPY b2b/site/css/effects/set2.css /var/www/b2b.wt18.ephec-ti.be/css/effects

COPY b2b/site/css/bootstrap.min.css /var/www/b2b.wt18.ephec-ti.be/css
COPY b2b/site/css/font-awesome.min.css /var/www/b2b.wt18.ephec-ti.be/css
COPY b2b/site/css/responsive.css /var/www/b2b.wt18.ephec-ti.be/css
COPY b2b/site/css/style.css /var/www/b2b.wt18.ephec-ti.be/css

COPY intranet/site/blog.html /var/www/intranet.wt18.ephec-ti.be/index.html

COPY intranet/site/images/blog-images/blog-2.jpg /var/www/intranet.wt18.ephec-ti.be/images/blog-images


COPY intranet/site/images/favicon.ico /var/www/intranet.wt18.ephec-ti.be/images
COPY intranet/site/images/logo.png /var/www/intranet.wt18.ephec-ti.be/images

COPY intranet/site/css/style.css /var/www/intranet.wt18.ephec-ti.be/css

EXPOSE 80 443

CMD apachectl -DFOREGROUND
