# Stage 1: build
FROM node:20-alpine AS builder
WORKDIR /app

# copy only package manifests to leverage cache
COPY package*.json ./

# install deps (falls back to npm install if npm ci isn't available)
RUN npm ci --silent || npm install --silent

# copy source and build
COPY . .
RUN npm run build

# Stage 2: serve with nginx (SPA fallback)
FROM nginx:alpine
# Remove default conf and replace with a simple SPA config
RUN rm -f /etc/nginx/conf.d/default.conf
RUN printf 'server {\n  listen 80;\n  server_name _;\n  root /usr/share/nginx/html;\n  index index.html;\n  location / { try_files $uri $uri/ /index.html; }\n}\n' > /etc/nginx/conf.d/default.conf

# copy built assets
COPY --from=builder /app/dist /usr/share/nginx/html

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]

