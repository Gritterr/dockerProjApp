# Forethought to-do app (Node.js + Express), listening on port 8080.
FROM node:20-alpine
WORKDIR /usr/src/app
ENV NODE_ENV=production

# Install dependencies before copying the code, so this layer is reused
# until package.json or package-lock.json changes
COPY package*.json ./
RUN npm ci --omit=dev

COPY . .
USER node
EXPOSE 8080

# Docker, and Swarm, mark the container unhealthy if the page stops loading
HEALTHCHECK --interval=10s --timeout=3s --start-period=5s --retries=3 \
  CMD wget -qO /dev/null http://localhost:8080/ || exit 1

CMD ["node", "index.js"]
