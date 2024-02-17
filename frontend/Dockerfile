FROM node:20.11.1-slim AS builder

# Add work directory
WORKDIR /react-app

COPY package.json .

RUN npm install

# Copy app files
COPY . .

# Build the app
RUN npm run build

# Separate stage for production image
FROM nginx:1.24.0-alpine as production
ENV NODE_ENV production

# Copy build directory
COPY --from=builder /react-app/build /usr/share/nginx/html

# Copy nginx.conf
COPY nginx.conf /etc/nginx/conf.d/default.conf

# Expose port
EXPOSE 80

# Start nginx
CMD ["nginx", "-g", "daemon off;"]