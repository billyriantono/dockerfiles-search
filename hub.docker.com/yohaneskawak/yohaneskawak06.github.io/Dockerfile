FROM alpine:latest
RUN apk add --update nginx && \
        rm -rf /var/cache/apk/* && \
        mkdir -p /tmp/nginx/

COPY files/nginx.conf /etc/nginx/nginx.conf
COPY files/default.conf /etc/nginx/conf.d/default.conf
ADD files/index.html /usr/share/nginx/html/
ADD files/css/bootstrap.min.css /usr/share/nginx/html/css/
ADD files/css/magnific-popup.css /usr/share/nginx/html/css/
ADD files/css/normalize.css /usr/share/nginx/html/css/
ADD files/css/owl.carousel.css /usr/share/nginx/html/css/
ADD files/css/owl.theme.css /usr/share/nginx/html/css/
ADD files/css/responsive.css /usr/share/nginx/html/css/
ADD files/css/style.css /usr/share/nginx/html/css/
ADD files/fonts/Glyphter.eot /usr/share/nginx/html/fonts/
ADD files/fonts/Glyphter.svg /usr/share/nginx/html/fonts/
ADD files/fonts/Glyphter.ttf /usr/share/nginx/html/fonts/
ADD files/fonts/Glyphter.woff /usr/share/nginx/html/fonts/
ADD files/images/blog-1.png /usr/share/nginx/html/images/
ADD files/images/blog-2.jpg /usr/share/nginx/html/images/
ADD files/images/blog-3.jpg /usr/share/nginx/html/images/
ADD files/images/blog-4.jpg /usr/share/nginx/html/images/
ADD files/images/blog-5.jpg /usr/share/nginx/html/images/
ADD files/images/blog-6.jpg /usr/share/nginx/html/images/
ADD files/images/bw-1.jpg /usr/share/nginx/html/images/
ADD files/images/bw-2.jpg /usr/share/nginx/html/images/
ADD files/images/bw-3.jpg /usr/share/nginx/html/images/
ADD files/images/bw-4.jpg /usr/share/nginx/html/images/
ADD files/images/bw-5.jpg /usr/share/nginx/html/images/
ADD files/images/bw-6.JPG /usr/share/nginx/html/images/
ADD files/images/favicon.ico /usr/share/nginx/html/images/
ADD files/images/hero1.jpeg /usr/share/nginx/html/images/
ADD files/images/loader.gif /usr/share/nginx/html/images/
ADD files/images/logo-big.png /usr/share/nginx/html/images/
ADD files/images/logo-bottom.jpg /usr/share/nginx/html/images/
ADD files/images/photography.jpg /usr/share/nginx/html/images/
ADD files/images/signature.png /usr/share/nginx/html/images/
ADD files/images/testimonial-bg.jpg /usr/share/nginx/html/images/
ADD files/images/yohan.jpg /usr/share/nginx/html/images/
ADD files/js/bootstrap.min.js /usr/share/nginx/html/js/
ADD files/js/classie.js /usr/share/nginx/html/js/
ADD files/js/html5shiv.min.js /usr/share/nginx/html/js/
ADD files/js/jquery.appear.js /usr/share/nginx/html/js/
ADD files/js/jquery.magnific-popup.min.js /usr/share/nginx/html/js/
ADD files/js/jquery-1.9.1.min.js /usr/share/nginx/html/js/
ADD files/js/main.js /usr/share/nginx/html/js/
ADD files/js/masonry.js /usr/share/nginx/html/js/
ADD files/js/masonry.pkgd.min.js /usr/share/nginx/html/js/
ADD files/js/owl.carousel.min.js /usr/share/nginx/html/js/
ADD files/js/smooth-scroll.min.js /usr/share/nginx/html/js/
ADD files/js/typed.js /usr/share/nginx/html/js/


EXPOSE 80/tcp

ENTRYPOINT ["nginx"]
CMD ["-g", "daemon off;"]
