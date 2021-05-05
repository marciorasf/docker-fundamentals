# Base image
FROM node:14.16.1-alpine 

# The dir that we will work inside the docker
WORKDIR /app

# Copy package.json and yarn.lock
# It's a good practice copy only this files first to use the Docker cache system
# Docker can identify if the commands have some changes
# If it doesn't have changes, it uses the cached layers
# This process can reduce significantly the build time
# As the dependencies do not change frequently, in most cases it will use the cache
COPY package.json .
COPY yarn.lock .

# Install the dependencies
RUN yarn

# Copy the other files
COPY . .

# Define environment variables
ENV PORT=8080

# Expose the port to communicate with the container outside
EXPOSE 8080

# Command that should be executed after the container creation
CMD ["node", "index.js"]