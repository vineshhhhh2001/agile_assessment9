# Use official Nginx image as base
FROM nginx:alpine

# Remove default nginx static content
RUN rm -rf /usr/share/nginx/html/*

# Copy our HTML application to nginx serve directory
COPY index.html /usr/share/nginx/html/index.html

# Expose port 80
EXPOSE 80

# Start Nginx in foreground
CMD ["nginx", "-g", "daemon off;"]
