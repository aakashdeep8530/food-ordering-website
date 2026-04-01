# Stage 1: Build / install dependencies
FROM node:18-alpine AS build
WORKDIR /app
# Copy package files
COPY package*.json ./
# Install all dependencies (including dev if needed for build)
RUN npm install
# Copy source code
COPY . .

# Stage 2: Production image
FROM node:18-alpine AS production
WORKDIR /app
# Copy only the dependencies needed for production
COPY package*.json ./
RUN npm install --production
# Copy source code from build stage
COPY --from=build /app ./
# Expose the port your server will run on
EXPOSE 4000
# Start the server
CMD ["node", "server.js"]