FROM cloudposse/github-authorized-keys@sha256:b3590fdd4c0b1753b5c93f99494c5b85109d1aeea34edb3261cdc6416ba867df as key-provider
FROM cloudposse/bastion@sha256:1b6e062c97dd0efb5129deed4fb3c0354d2163d128136685acdac48b82de6bf1

COPY --from=key-provider /usr/bin/github-authorized-keys /usr/bin/github-authorized-keys

CMD ["/usr/bin/github-authorized-keys &;/init"]