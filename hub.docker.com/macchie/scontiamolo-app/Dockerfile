# Use Nginx Alpine Image
FROM nginx:alpine

# Create app directory
WORKDIR /usr/share/nginx/html

# Copy dependencies
COPY ./www .

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
