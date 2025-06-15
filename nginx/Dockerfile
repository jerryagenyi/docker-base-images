FROM nginx:latest

# Create default configuration
RUN echo 'server { \n\
    listen 80; \n\
    server_name localhost; \n\
    \n\
    location / { \n\
        root /usr/share/nginx/html; \n\
        index index.html; \n\
        try_files $uri $uri/ /index.html; \n\
    } \n\
}' > /etc/nginx/conf.d/default.conf.template

# Copy configuration if it exists, otherwise use default
COPY <<-"EOT" /docker-entrypoint.d/40-create-config.sh
#!/bin/sh
if [ -f /etc/nginx/custom.conf ]; then
    cp /etc/nginx/custom.conf /etc/nginx/conf.d/default.conf
else
    cp /etc/nginx/conf.d/default.conf.template /etc/nginx/conf.d/default.conf
fi
EOT

RUN chmod +x /docker-entrypoint.d/40-create-config.sh

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]