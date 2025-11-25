# Vite React Workflows Demo

A demonstration project showcasing GitHub Actions CI/CD workflows with a React application built using Vite.

## 📋 Project Overview

This project is an educational application that teaches users about Git, GitHub, and GitHub Actions. It features a clean, interactive UI built with React and Vite, complete with automated testing and deployment workflows.

## 🎯 Features

- **Interactive Help System**: Toggle-able help sections explaining Git, GitHub, and GitHub Actions
- **Component-Based Architecture**: Modular React components with reusable help boxes
- **Automated Testing**: Unit tests using Vitest and React Testing Library
- **GitHub Actions CI/CD**: Multi-job workflows with automated testing and deployment
- **Modern Build Tools**: Vite for fast development and optimized production builds

## 🚀 Getting Started

### Prerequisites

- Node.js 18 or higher
- npm or yarn

### Installation

```bash
npm install
```

### Development

Start the development server:

```bash
npm run dev
```

The application will be available at `http://localhost:5173`

### Building

Create a production build:

```bash
npm run build
```

### Testing

Run the test suite:

```bash
npm test
```

## 📁 Project Structure

```
├── src/
│   ├── components/
│   │   ├── MainContent.jsx      # Main content container with help toggle
│   │   ├── HelpArea.jsx         # Help section with multiple help items
│   │   ├── HelpBox.jsx          # Individual help box component
│   │   ├── MainContent.test.jsx # Component tests
│   │   ├── HelpArea.css
│   │   ├── HelpBox.css
│   │   └── MainContent.test.jsx
│   ├── assets/
│   │   └── images/              # Static images
│   ├── App.jsx                  # Root application component
│   ├── main.jsx                 # Application entry point
│   └── index.css                # Global styles
├── .github/
│   └── workflows/
│       ├── deployment.yml       # Multi-job CI/CD workflow
│       └── output.yml           # Output GitHub context workflow
├── vite.config.js               # Vite configuration
├── index.html                   # HTML entry point
└── package.json                 # Project dependencies and scripts
```

## 🔧 Technologies Used

- **Frontend Framework**: React 18
- **Build Tool**: Vite 3
- **Testing**: Vitest, React Testing Library, Jest DOM
- **CI/CD**: GitHub Actions
- **Styling**: CSS3

## 📦 Available Scripts

| Script            | Description                      |
| ----------------- | -------------------------------- |
| `npm run dev`     | Start development server         |
| `npm run build`   | Create production build          |
| `npm run preview` | Preview production build locally |
| `npm test`        | Run test suite                   |

## 🔄 GitHub Actions Workflows

### Deployment Workflow (`.github/workflows/deployment.yml`)

A sophisticated multi-job workflow that ensures code quality before deployment.

#### **Workflow Structure**

The deployment workflow consists of two distinct jobs:

- **`test` Job**: Runs the project's automated test suite
- **`deploy` Job**: Builds production assets and deploys them (only runs if tests pass)

The `deploy` job is configured with `needs: test` to ensure it only executes if all tests succeed.

#### **Test Job Steps**

| Step                     | Implementation                                        | Rationale                                                                                                                                             |
| ------------------------ | ----------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Download Code**        | `uses: actions/checkout@v3`                           | The runner is a clean environment and must first fetch the repository's source code to work with it                                                   |
| **Setup NodeJS**         | `uses: actions/setup-node@v3` with `node-version: 18` | Installs and configures Node.js 18, ensuring a consistent environment regardless of the runner's default version                                      |
| **Install Dependencies** | `run: npm ci`                                         | Installs dependencies from `package-lock.json`. `npm ci` is preferred in CI environments for faster, more reliable builds using exact locked versions |
| **Run Tests**            | `run: npm test`                                       | Executes the project's automated test suite. If any test fails, this job fails, preventing the deploy job from running                                |

#### **Deploy Job Steps**

| Step                     | Implementation                                        | Rationale                                                                               |
| ------------------------ | ----------------------------------------------------- | --------------------------------------------------------------------------------------- |
| **Download Code**        | `uses: actions/checkout@v3`                           | Each job runs on a separate runner, so the code must be checked out again               |
| **Setup NodeJS**         | `uses: actions/setup-node@v3` with `node-version: 18` | Ensures the correct Node.js environment for the build process                           |
| **Install Dependencies** | `run: npm ci`                                         | Dependencies are required for the build step                                            |
| **Build Project**        | `run: npm run build`                                  | Compiles source code and bundles assets for production                                  |
| **Deploy**               | `run: echo "Deploying..."`                            | Simulates deployment. In production, this would upload built assets to a hosting server |

#### **Workflow Execution Flow**

```
Push to Repository
        ↓
    [Test Job]
   ✓ Checkout
   ✓ Setup Node.js
   ✓ Install Dependencies
   ✓ Run Tests
        ↓
   Tests Pass?
   ├─ YES → [Deploy Job] → Build & Deploy
   └─ NO  → Workflow Stops (Deploy doesn't run)
```

### Output Workflow (`.github/workflows/output.yml`)

Manual trigger workflow to display GitHub context information for debugging and learning purposes.

## 📚 Components

- **`App`** (`src/App.jsx`): Root component with header and logo
- **`MainContent`** (`src/components/MainContent.jsx`): Container managing help visibility state
- **`HelpArea`** (`src/components/HelpArea.jsx`): Displays collection of help items
- **`HelpBox`** (`src/components/HelpBox.jsx`): Reusable component for individual help items

## ✅ Testing

The project includes unit tests for the `MainContent` component using React Testing Library:

- Tests button rendering
- Tests help area visibility toggle functionality

Run tests with: `npm test`

## 🔐 Key Workflow Benefits

- **Quality Assurance**: Tests must pass before deployment
- **Consistency**: Same Node.js version across all environments
- **Reliability**: Lock file usage prevents dependency version issues
- **Efficiency**: Multi-job structure allows parallel execution where applicable
- **Safety**: Failed tests automatically prevent faulty deployments

## 📄 License

This project is provided as-is for educational purposes.

---

**Last Updated**: November 25, 2025
