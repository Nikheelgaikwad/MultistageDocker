# First stage: Build the application
FROM node:16 AS builder

# Set the working directory inside the container
WORKDIR /app

# Copy package.json and package-lock.json files to the working directory
COPY package*.json ./

# Install the dependencies
RUN npm install

# Copy the rest of the application code to the working directory
COPY . .

# Build the application (dummy build step for this example)
RUN npm run build

# Second stage: Create a lightweight image for running the application
FROM node:16-alpine

# Set the working directory inside the container
WORKDIR /app

# Copy the built application from the builder stage
COPY --from=builder /app/dist ./dist

# Copy package.json and package-lock.json files to the working directory
COPY package*.json ./

# Install only production dependencies
RUN npm install --only=production

# Expose the application port
EXPOSE 3000

# Command to run the application
CMD ["npm", "start"]
