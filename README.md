# git-hooks

A collection of useful Git hooks to streamline and automate various tasks during development. This repository can be extended over time with new hooks as needed.

## How to Use

1. Clone this repository into your project or set it up as a global hook repository.
2. Configure Git to use the hooks by setting the `core.hooksPath` in your `.gitconfig`:

   ```bash
   git config core.hooksPath /path/to/your/git-hooks/repo
   ```

3. Place each hook in the corresponding file (e.g., `pre-commit`, `pre-push`, etc.).
4. Make the hooks executable by running:

   ```bash
   chmod +x /path/to/your/git-hooks/repo/*
   ```

---

## Available Hooks

### 1. **Pre-Commit Hook: Lint and Auto-Fix (Node.js Projects)**
   - **File**: `pre-commit`
   - **Description**: This hook runs ESLint (via Nx) on changed JavaScript and TypeScript files when a commit is attempted. It attempts to auto-fix any issues, and if some errors remain unfixed, it aborts the commit and displays the errors. If the linter successfully fixes the issues, the modified files are automatically staged for commit.
   - **Features**:
     - Runs only on **changed** and **staged** files.
     - Automatically **stages fixed** files after linting.
     - Works in **silent mode**, suppressing unnecessary output.
     - Ensures the project is a **Node.js project** by checking for a `package.json` file.
     - Aborts the commit if **npx or nx** is not installed, with instructions for installation.
   - **How It Works**:
     - The hook identifies modified files using `git diff --cached` and runs the linter only on those files.
     - The linter fixes issues and stages the fixed files automatically.
     - The commit is aborted if errors can't be auto-fixed.
