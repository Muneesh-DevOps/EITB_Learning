# Stage 1: Build the React app
FROM node:18 AS build

WORKDIR /app

# Install dependencies
COPY package*.json ./
RUN npm install

# Copy app source and build
COPY . .
RUN npm run build

# Stage 2: Serve the built app using nginx
FROM nginx:alpine

# Remove the default nginx static files
RUN rm -rf /usr/share/nginx/html/*

# Copy build files from the React app
COPY --from=build /app/build /usr/share/nginx/html

# Expose nginx port
EXPOSE 80

# Start nginx
CMD ["nginx", "-g", "daemon off;"]
