# ---- Build Stage ----
FROM node AS build

# Set the working directory
WORKDIR /frontend

# Copy the package.json and package-lock.json
COPY package*.json .

# Copy the frontend code
COPY . .

# Install dependencies and build app
RUN npm install

RUN npm run build

# ---- Production Stage ----
FROM nginx:alpine

# Set the working directory in nginx
WORKDIR /usr/share/nginx/html

# Remove default nginx static assets
RUN rm -rf ./*

# Copy static assets from builder stage
COPY --from=build /frontend/build .

# Containers run nginx with global directives and daemon off
CMD ["nginx", "-g", "daemon off;"]
