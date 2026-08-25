# Official Node image
FROM node:24-alpine

WORKDIR /app

# Install dependencies
COPY package*.json ./
RUN npm i

# Copy the project
COPY . .

# Expose port
EXPOSE 5173

# Launch dev server (port 5173)
CMD ["npm", "run", "dev", "--", "--host"]
