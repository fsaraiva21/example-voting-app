FROM node:18-slim

ENV PORT 80
EXPOSE 80

# Add curl for healthcheck and tini for signal handling 
RUN apt-get update \
    && apt-get install -y --no-install-recommends \
    curl \
    tini \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /app

# Install nodemon for local dev use (file watching)
RUN npm install -g nodemon@2.*

# Copy in package dependencies
COPY package*.json ./

# Install package dependencies
RUN npm ci \
 && npm cache clean --force \
 # move node_modules up a directory so they still work with bind-mounted code in development
 && mv /app/node_modules /node_modules

# Copy code from the current folder to /app inside the container
COPY . .

# Define launch command using tini
CMD ["tini", "--", "node", "server.js"]
