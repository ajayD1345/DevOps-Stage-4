# Stage 1: build the vue.js application
FROM node:14-alpine3.14 AS build-stage
WORKDIR /app

# Install required build tools for node-sass
#RUN apk add --no-cache python2 make g++ && \
#    ln -sf python2 /usr/bin/python

# Install the application dependencies
COPY package*.json ./
RUN npm install --legacy-peer-deps

# Copy in the source code
COPY . .
RUN npm run build

# Stage 2: serve the app with nginx
FROM nginx:stable-alpine AS production-stage

# Copy the built Vue.js files into Nginx's default directory
COPY --from=build-stage /app/dist /usr/share/nginx/html

# Expose port 80 – Traefik will forward HTTPS requests here
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]

