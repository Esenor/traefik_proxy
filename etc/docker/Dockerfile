FROM traefik:2.2
RUN mkdir -p /etc/traefik/dynamicConfiguration
RUN mkdir -p /letsencrypt/
COPY etc/traefik/traefik.yml etc/traefik/traefik.yml
COPY etc/traefik/dynamicConfiguration/config.yml etc/traefik/dynamicConfiguration/config.yml
CMD ["traefik"]