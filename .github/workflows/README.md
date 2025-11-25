
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

