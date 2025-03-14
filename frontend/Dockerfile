# Stage 1: Build the application
FROM node:alpine AS build


# Copy package.json and package-lock.json (if available)
COPY package.json package-lock.json ./
RUN npm install

# Copy the rest of the application code
COPY . .

# Build the application
RUN npm run build

# Stage 2: Serve the application with Nginx
FROM nginx:stable-alpine

# Copy the built application from the build stage
COPY --from=build /dist /usr/share/nginx/html

# Copy the Nginx configuration file
COPY --from=build /nginx.conf /etc/nginx/conf.d/default.conf

# Expose the port that Nginx will run on
EXPOSE 3000

# Start Nginx
CMD ["nginx", "-g", "daemon off;"]