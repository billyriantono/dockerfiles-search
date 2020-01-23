FROM ajones17/frr:662 as frr_pkgs

FROM alpine:3.7
COPY --from=frr_pkgs /pkgs/apk/x86_64/frr-6.1_git1042702486119-r0.apk /frr-6.1_git1042702486119-r0.apk
RUN apk add --no-cache --allow-untrusted /frr-6.1_git1042702486119-r0.apk
