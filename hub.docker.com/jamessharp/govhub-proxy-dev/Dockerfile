FROM nginx:1.9

# Expose port 80
EXPOSE 443

# Add in the config
COPY nginx.conf /etc/nginx/nginx.conf
COPY dev.governorhub.com.pem /etc/ssl/dev.governorhub.com.pem
COPY dev.governorhub.com.chain.crt /etc/ssl/dev.governorhub.com.chain.crt
COPY dev.earlyyearshub.com.pem /etc/ssl/dev.earlyyearshub.com.pem
COPY dev.earlyyearshub.com.chain.crt /etc/ssl/dev.earlyyearshub.com.chain.crt
