# ---------- Stage 1: Dependencies ----------
FROM node:20-alpine AS deps

WORKDIR /app

COPY package*.json ./

# Install only production dependencies
RUN npm ci --omit=dev

# ---------- Stage 2: Runtime ----------
FROM node:20-alpine

WORKDIR /app

# Copy node_modules from deps stage
COPY --from=deps /app/node_modules ./node_modules

# Copy application code
COPY . .

# Use non-root user (security best practice)
USER node

# Expose your backend port
EXPOSE 5000

# Start application
CMD ["node", "server.js"]
