FROM node:18
WORKDIR /app

# Install common development packages
RUN npm install -g nodemon typescript ts-node prettier eslint

# Create a package.json if one doesn't exist
RUN echo '{"name":"app","version":"1.0.0","private":true}' > /app/package.json.default

# Script to check for package.json and install dependencies
COPY <<-"EOT" /app/docker-entrypoint.sh
#!/bin/sh
if [ ! -f package.json ]; then
    cp package.json.default package.json
fi
if [ -f package.json ]; then
    npm install
fi
exec "$@"
EOT

RUN chmod +x /app/docker-entrypoint.sh

ENTRYPOINT ["/app/docker-entrypoint.sh"]
CMD ["node", "server.js"]