# Use an official Node.js image as the base image
FROM node:18-alpine AS build

# Set the working directory in the container
WORKDIR /app

# Copy package.json and package-lock.json (or yarn.lock)
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the application code
COPY . .

# Build the React app for production
RUN npm run build

# Use an Nginx server to serve the React app
FROM nginx:alpine

# Copy the build output from the previous stage to the Nginx server's web directory
COPY --from=build /app/build /usr/share/nginx/html

# Expose the port Nginx will run on
EXPOSE 80

# Command to run Nginx
CMD ["nginx", "-g", "daemon off;"]