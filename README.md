# MongoDB Dockerfile:
```bash
# Use the official MongoDB image as the base image
FROM mongo:latest

# Expose MongoDB port
EXPOSE 27017
```
# Backend Dockerfile:
  ```bash
# Use the official NodeJS image as the base image
  FROM node:latest

# Set working directory
WORKDIR /app

# Copy package.json and package-lock.json
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy server files
COPY . .

# Expose port
EXPOSE 5000

# Command to run the server
CMD ["node", "index.js"]

  ```
# FrontEnd Dockerfile:
  ```bash
  # Use Node.js image as base
FROM node:latest AS build

# Set working directory
WORKDIR /app

# Copy package.json and package-lock.json
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the ReactJS application files
COPY . .

# Build the React app
RUN npm run build

# Production environment
FROM nginx:alpine

# Copy build files to Nginx
COPY --from=build /app/build /usr/share/nginx/html

# Expose port
EXPOSE 80
```
