# Makeflow Toolkit 🚀

> A production-ready **Next.js 15 & React 19** starter kit powered by modular **Makefile** DX automation and **pnpm 10**.

Stop wrestling with complex local setups, inconsistent package manager scripts, or messy Docker builds. **Makeflow Toolkit** provides a unified, developer-friendly command-line interface wrapped around a modern web stack.

---

## ✨ Features

- ⚡ **Next.js 15 & React 19** — App Router, Server Components, and optimized performance.
- 🛠️ **DX Automation via Makefile** — Standardized, modular commands (`make setup`, `make check`, `make dev`).
- 📦 **pnpm 11 Ready** — Pre-configured with pnpm-workspace.yaml for strict build-script permissions.
- 🎨 **Tailwind CSS & Dark Mode** — Clean styling setup with CSS module declarations out-of-the-box.
- 🛡️ **TypeScript (ES2022)** — Strict type safety without IDE friction or side-effect import warnings.
- 🧪 **Testing & Quality Assurance** — Pre-configured pipeline with **Vitest**, **ESLint 9**, and **Prettier**.
- 🐳 **Production Docker Setup** — Multi-stage builds utilizing Next.js `standalone` output.

---

## 📁 Project Structure

```text
.
├── Makefile                # Main Entrypoint (Includes modular scripts from make/)
├── make/                   # Modular Makefile scripts
│   ├── 00-config.mk        # Environment & variables
│   ├── 01-dev.mk           # Development & setup targets
│   ├── 02-docker.mk        # Container management
│   └── 03-quality.mk       # Linting, formatting & testing
├── pnpm-workspace.yaml     # pnpm 10 build script permissions
├── tsconfig.json           # Modern TypeScript (ES2022) configuration
├── Dockerfile              # Multi-stage production build
└── src/
    ├── app/                # App Router (layout, page, error handlers)
    └── styles/             # Global Tailwind & CSS definitions
```

---

## 🚀 Quick Start

### Prerequisites

Make sure you have the following installed on your machine:

- **Node.js**: `>= 20.0.0`
- **pnpm**: `>= 11.0.0` (v11 fully supported)
- **Make**: Available natively on macOS/Linux (or via WSL/Git Bash on Windows)

### 1. Clone & Setup

```bash
git clone [https://github.com/your-username/makeflow-toolkit.git](https://github.com/your-username/makeflow-toolkit.git)
cd makeflow-toolkit

# Run system checks, copy .env, and install dependencies
make setup
```

### 2. Start Development Server

```bash
make dev
```

Open [http://localhost:3000](http://localhost:3000) in your browser to view the application.

---

## 🛠️ Command Line Interface (Makefile Reference)

Instead of remembering long CLI flags, use the streamlined `make` targets:

| Command       | Description                                                                 |
| :------------ | :-------------------------------------------------------------------------- |
| `make setup`  | Verifies system tools, copies environment variables, and installs packages. |
| `make dev`    | Starts the Next.js development server with Turbopack.                       |
| `make check`  | Runs the full quality suite: TypeScript type-check, ESLint, and Vitest.     |
| `make format` | Formats all files across the project using Prettier.                        |
| `make build`  | Builds the production Next.js application locally.                          |
| `make up`     | Builds and starts the Docker container in detached mode.                    |
| `make down`   | Stops and removes active Docker containers.                                 |
| `make clean`  | Purges `.next`, `node_modules`, and build artifacts.                        |

---

## 🐳 Docker Deployment

To spin up a containerized production build locally:

```bash
make up
```

This runs a multi-stage Docker build that isolates dependencies and leverages Next.js standalone output for minimal image size. To stop the container, run:

```bash
make down
```

---

## 📄 License

This project is licensed under the [MIT License](LICENSE).

---

<p align="center">
  Crafted with ❤️ by <b>SvenCodesSimple</b>
</p>
