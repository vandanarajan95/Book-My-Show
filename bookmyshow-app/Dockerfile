# Step 1: Use Node to build the app
FROM node:18-alpine AS builder
WORKDIR /app
COPY package*.json ./
# Use --legacy-peer-deps to ignore version conflicts
RUN npm install --legacy-peer-deps
COPY . .
RUN npm run build

# Step 2: Use a clean, tiny image to serve the build
FROM node:18-alpine
WORKDIR /app
# Install a simple web server
RUN npm install -g serve
# Only copy the final built files from the builder
COPY --from=builder /app/build ./build

EXPOSE 3000
# Serve the build folder on port 3000
CMD ["serve", "-s", "build", "-l", "3000"]
