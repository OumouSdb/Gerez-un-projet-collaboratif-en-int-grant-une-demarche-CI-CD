# Use a stable Node.js LTS version for the build stage
FROM node:18 as build

# Set the working directory inside the container
WORKDIR /usr/local/app

# Copy the application files to the container
COPY ./ /usr/local/app/

# Install dependencies
RUN yarn

# Build the Angular application
RUN npm run build

# Use the latest NGINX image for the production stage
FROM nginx:latest as production

# Copy custom NGINX configuration
COPY nginx.conf /etc/nginx/conf.d/default.conf

# Copy built application from the build stage
COPY --from=build /usr/local/app/dist/bobapp /usr/share/nginx/html

# Expose port 80 for the application
EXPOSE 80
