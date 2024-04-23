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
