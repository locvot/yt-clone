#Stage 1: Build stage
FROM node:18 AS builder

# Set the working directory
WORKDIR /app

# Copy the package.json file
copy package*.json ./

# Install the dependencies
RUN npm install

# Copy the source code
COPY  . .

# Build the application
RUN npm run build

#Stage 2: Production stage
FROM node:18

# Install ffmpeg in the container
RUN apt-get update && apt-get install -y ffmpeg

# Set the working directory
WORKDIR /app

# Copy the package.json file
COPY package*.json ./

# Install only production dependencies
RUN npm install --only=production

# Copy the build files from the builder stage
COPY --from=builder /app/dist ./dist

# Expose the port
EXPOSE 3000

# Define the command
CMD ["npm", "run", "serve"]