FROM node:18-alpine AS builder
WORKDIR /app
COPY package*.json ./
RUN npm ci 
COPY ..
RUN npm run build   # produces /app/build (adjust if different)

# Serve with nginx
FROM nginx:stable-alpine
# Remove default config and add our own if needed
RUN rm -rf /usr/share/nginx/html/*
COPY --from=builder /app/build /usr/share/nginx/html
# Optional: copy nginx config if you have custom one
# COPY nginx.conf /etc/nginx/conf.d/default.conf

# Expose port used by nginx
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
