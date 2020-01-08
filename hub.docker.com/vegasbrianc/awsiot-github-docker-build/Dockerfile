FROM nginx:latest

#COPY index.html /usr/share/nginx/html
COPY index-new.html /usr/share/nginx/html/index.html

# Add new content
#COPY linux.png /usr/share/nginx/html
COPY 56kcloud_logo.png /usr/share/nginx/html

EXPOSE 80 443 	

CMD ["nginx", "-g", "daemon off;"]
