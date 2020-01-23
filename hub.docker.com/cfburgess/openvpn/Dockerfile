# Original credit: https://github.com/kylemanna/docker-openvpn

# Smallest base image
FROM alpine:latest

LABEL maintainer="Chet Burgess <cfb@liquidreality.org>"

# Install our packages
RUN apk add --update openvpn \
                     iptables \
                     bash \
                     easy-rsa \
                     openvpn-auth-pam \
                     google-authenticator \
                     python3 \
                     py3-yaml && \
    rm -rf /tmp/* /var/tmp/* /var/cache/apk/* /var/cache/distfiles/* /etc/openvpn/*

# Copy our exec script
ADD ./bin/run-vpn /usr/local/bin/run-vpn
RUN chmod 555 /usr/local/bin/run-vpn

# Add support for OTP authentication using a PAM module
ADD ./otp/openvpn /etc/pam.d/

# Execute openvpn
CMD ["/usr/local/bin/run-vpn"]
