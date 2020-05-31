FROM traefik:2.2
RUN mkdir -p /etc/traefik/dynamicConfiguration
COPY etc/traefik/traefik.yml etc/traefik/traefik.yml
COPY etc/traefik/dynamicConfiguration/config.yml etc/traefik/dynamicConfiguration/config.yml
RUN ls -alh /etc/traefik
RUN ls -alh /etc/traefik/dynamicConfiguration
CMD ["traefik"]