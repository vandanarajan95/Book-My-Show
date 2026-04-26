# Step 1: Use Node to build the app
FROM node:18-alpine AS builder
WORKDIR /app
COPY package*.json ./
RUN npm install --legacy-peer-deps

# THE FIX IS HERE: Set the environment variable for the build process
ENV NODE_OPTIONS=--openssl-legacy-provider

COPY . .
RUN npm run build

# Step 2: Use a clean, tiny image to serve the build
FROM node:18-alpine
WORKDIR /app
RUN npm install -g serve
COPY --from=builder /app/build ./build

EXPOSE 3000
CMD ["serve", "-s", "build", "-l", "3000"]
