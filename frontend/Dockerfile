# Stage 1: Build the frontend
FROM node:18 AS builder
WORKDIR /app

# Copy package.json and lock file first (for better caching)
COPY package.json ./
RUN yarn install --frozen-lockfile  || yarn install

# Copy everything else and build the frontend
COPY . .
RUN yarn build

# Stage 2: Serve with Nginx
FROM nginx:alpine
COPY --from=builder /app/dist /usr/share/nginx/html
 
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
 