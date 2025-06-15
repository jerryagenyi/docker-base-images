FROM caddy:latest

# Create default Caddyfile
RUN echo ':80 {\n\
    respond "Caddy default page. Mount your custom Caddyfile to /etc/caddy/Caddyfile"\n\
}' > /etc/caddy/Caddyfile.default

# Copy configuration management script
COPY <<-"EOT" /usr/local/bin/docker-entrypoint.sh
#!/bin/sh
if [ ! -f /etc/caddy/Caddyfile ]; then
    cp /etc/caddy/Caddyfile.default /etc/caddy/Caddyfile
fi

# Format Caddyfile
caddy fmt --overwrite /etc/caddy/Caddyfile

exec "$@"
EOT

RUN chmod +x /usr/local/bin/docker-entrypoint.sh

WORKDIR /srv
EXPOSE 80 443 2019
VOLUME /data
VOLUME /config

ENTRYPOINT ["/usr/local/bin/docker-entrypoint.sh"]
CMD ["caddy", "run", "--config", "/etc/caddy/Caddyfile", "--adapter", "caddyfile"]