# Vite React Workflows Demo

A demonstration project showcasing GitHub Actions CI/CD workflows with a React application built using Vite.

## 📋 Project Overview

This project is an educational application that teaches users about Git, GitHub, and GitHub Actions. It features a clean, interactive UI built with React and Vite, complete with automated testing and deployment workflows.

## 🎯 Features

- **Interactive Help System**: Toggle-able help sections explaining Git, GitHub, and GitHub Actions
- **Component-Based Architecture**: Modular React components with reusable help boxes
- **Automated Testing**: Unit tests using Vitest and React Testing Library
- **GitHub Actions CI/CD**: Automated testing and deployment workflows
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
│       ├── deployment.yml       # Deploy workflow with tests
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

### Deployment Workflow (deployment.yml)

Runs on every push and manual trigger:

1. **Test Job**: Checks out code, installs dependencies, and runs tests
2. **Deploy Job**: Builds the project and deploys (depends on test success)

### Output Workflow (output.yml)

Manual trigger to display GitHub context information for debugging.

## 📚 Components

- **`App`**: Root component with header and logo
- **`MainContent`**: Container managing help visibility state
- **`HelpArea`**: Displays collection of help items
- **`HelpBox`**: Reusable component for individual help items

## ✅ Testing

The project includes unit tests for the `MainContent` component using React Testing Library:

- Tests button rendering
- Tests help area visibility toggle functionality

Run tests with: `npm test`

## 📄 License

This project is provided as-is for educational purposes.
