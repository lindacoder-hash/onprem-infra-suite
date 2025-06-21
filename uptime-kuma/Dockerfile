# Use Node.js as the base image
FROM node:20

# Set working directory
WORKDIR /app

# Clone the Uptime Kuma repository
RUN git clone https://github.com/louislam/uptime-kuma.git .

# Change directory to the correct folder
WORKDIR /app

# Update from git
RUN git fetch --all && git checkout 1.23.16 --force

# Install dependencies and prebuilt assets
RUN npm install --production && npm run download-dist

# Install PM2 globally and setup log rotation
RUN npm install -g pm2 && pm2 install pm2-logrotate

# Expose the default port
EXPOSE 3001

# Start Uptime Kuma using PM2
CMD ["pm2-runtime", "start", "server/server.js", "--name", "uptime-kuma"]
