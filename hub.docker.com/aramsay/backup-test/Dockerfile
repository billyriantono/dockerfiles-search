FROM nginx:alpine

RUN apk --update add bash && rm -rf /var/cache/apk/*

RUN chown nginx:nginx /var/run

COPY ["default.conf", "/etc/nginx/conf.d/default.conf"]
COPY ["index.html", "/usr/share/nginx/html/index.html"]
COPY ["assets/a.png", "/usr/share/nginx/html/a/test.png"]
COPY ["assets/b.png", "/usr/share/nginx/html/b/test.png"]
COPY ["assets/c.png", "/usr/share/nginx/html/c/test.png"]
COPY ["assets/d.png", "/usr/share/nginx/html/d/test.png"]

COPY ["drunner", "/drunner"]

USER nginx

EXPOSE 8000

CMD ["nginx", "-g", "daemon off;"]
