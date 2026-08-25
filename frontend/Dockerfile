# syntax=docker/dockerfile:1

ARG NODE_VERSION=24-alpine

# ============================================================
# BASE
# ============================================================

FROM node:${NODE_VERSION} AS base

# The workdir name appears in the compose.yml
WORKDIR /app

# Install dependencies
RUN --mount=type=cache,target=/root/.npm \
    --mount=type=bind,source=package.json,target=package.json \
    --mount=type=bind,source=package-lock.json,target=package-lock.json \
    npm ci


# ============================================================
# DEVELOPMENT
# ============================================================

FROM base AS development

# Copy source code
COPY . .

EXPOSE 5173

CMD ["npm", "run", "dev", "--", "--host"]