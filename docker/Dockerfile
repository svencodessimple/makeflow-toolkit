# ==========================================
# Multi-Stage Dockerfile for Next.js Standalone
# Path: docker/Dockerfile
# ==========================================

# 1. Base stage - Shared Node/Alpine setup
FROM node:22-alpine AS base
WORKDIR /app

# Install libc6-compat for native dependency compatibility on Alpine
RUN apk add --no-cache libc6-compat

# CI-Modus aktivieren (verhindert ERR_PNPM_ABORTED_REMOVE_MODULES_DIR_NO_TTY in pnpm 11)
ENV CI=true

# Enable Corepack and prepare pnpm 11
ENV PNPM_HOME="/pnpm"
ENV PATH="$PNPM_HOME:$PATH"
RUN corepack enable && corepack prepare pnpm@11.18.0 --activate


# 2. Dependencies stage - Install production & dev dependencies
FROM base AS deps
WORKDIR /app

# Copy package manifests for optimal layer caching
COPY package.json pnpm-lock.yaml* pnpm-workspace.yaml* ./

# Install dependencies deterministically based on lockfile
RUN pnpm i --frozen-lockfile


# 3. Builder stage - Compile the Next.js application
FROM base AS builder
WORKDIR /app

COPY --from=deps /app/node_modules ./node_modules
COPY . .

# Disable Next.js telemetry during build time
ENV NEXT_TELEMETRY_DISABLED=1
ENV NODE_ENV=production

# Build the application (requires output: "standalone" in next.config.mjs)
RUN pnpm build


# 4. Runner stage - Production-ready minimal image
FROM base AS runner
WORKDIR /app

ENV NODE_ENV=production
ENV NEXT_TELEMETRY_DISABLED=1
ENV PORT=3000
ENV HOSTNAME="0.0.0.0"

# Create a dedicated non-root system user for security
RUN addgroup --system --gid 1001 nodejs && \
    adduser --system --uid 1001 nextjs

# Copy static public assets
COPY --from=builder /app/public ./public

# Set up correct permissions for Next.js image optimization cache
RUN mkdir .next && \
    chown nextjs:nodejs .next

# Copy standalone build output & static files
COPY --from=builder --chown=nextjs:nodejs /app/.next/standalone ./
COPY --from=builder --chown=nextjs:nodejs /app/.next/static ./.next/static

# Switch to non-root user
USER nextjs

EXPOSE 3000

# Start Next.js standalone Node server
CMD ["node", "server.js"]