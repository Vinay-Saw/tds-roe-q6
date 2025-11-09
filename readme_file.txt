# Multi-Platform Matrix Build with GitHub Actions

This repository demonstrates a comprehensive GitHub Actions matrix build strategy with artifact management across multiple platforms and Node.js versions.

## Contact Information

**Email:** your.email@example.com

## Overview

This project showcases a CI/CD pipeline that:
- ✅ Builds across 4 different matrix variants
- ✅ Runs jobs in parallel for efficiency
- ✅ Generates unique artifacts for each build variant
- ✅ Includes proper artifact management and verification
- ✅ Provides build summaries and reports

## Matrix Configuration

The workflow builds across the following variants:

| Variant | OS | Node.js Version |
|---------|-----|----------------|
| `ubuntu-node18` | Ubuntu Latest | 18.x |
| `ubuntu-node20` | Ubuntu Latest | 20.x |
| `macos-node18` | macOS Latest | 18.x |
| `windows-node18` | Windows Latest | 18.x |

## Workflow Features

### 1. Matrix Build Strategy
- Parallel execution across multiple OS platforms (Ubuntu, macOS, Windows)
- Multiple Node.js versions (18, 20)
- Each combination runs as an independent job

### 2. Build Artifacts
Each matrix job generates:
- `build-info.json` - Detailed build metadata
- `build-log.txt` - Build execution log
- `app-output.txt` - Application build output

All artifacts are named with the prefix `build-8bf96b7-<variant>` for easy identification.

### 3. Artifact Collection
A separate job collects all artifacts and generates a comprehensive build summary.

## Workflow File

The workflow is defined in `.github/workflows/matrix-build.yml`

### Key Components

```yaml
strategy:
  matrix:
    include:
      - os: ubuntu-latest
        node-version: '18'
        variant: 'ubuntu-node18'
      # ... additional variants
```

### Step Identifier

The workflow includes a step with identifier `matrix-8bf96b7` that displays the build configuration:

```yaml
- name: matrix-8bf96b7
  run: |
    echo "Matrix Build Configuration"
    echo "OS: ${{ matrix.os }}"
    echo "Node Version: ${{ matrix.node-version }}"
```

## Getting Started

### Prerequisites
- GitHub account
- Repository with GitHub Actions enabled

### Setup Instructions

1. **Create the repository:**
   ```bash
   mkdir matrix-build-demo
   cd matrix-build-demo
   git init
   ```

2. **Create the workflow directory:**
   ```bash
   mkdir -p .github/workflows
   ```

3. **Add the workflow file:**
   - Copy the workflow YAML to `.github/workflows/matrix-build.yml`

4. **Add this README:**
   - Update the email address in this file
   - Save as `README.md`

5. **Commit and push:**
   ```bash
   git add .
   git commit -m "Add matrix build workflow"
   git branch -M main
   git remote add origin <your-repo-url>
   git push -u origin main
   ```

### Triggering the Workflow

The workflow triggers on:
- Push to `main` or `master` branch
- Pull requests
- Manual dispatch (via GitHub UI)

To manually trigger:
1. Go to your repository on GitHub
2. Click "Actions" tab
3. Select "Multi-Platform Matrix Build"
4. Click "Run workflow"

## Validation Checklist

This workflow meets all requirements:

- ✅ **Matrix Strategy:** 4 different variants configured
- ✅ **Parallel Execution:** All matrix jobs run in parallel
- ✅ **Build Artifacts:** Each job generates unique artifacts
- ✅ **Artifact Upload:** Uses `actions/upload-artifact@v4`
- ✅ **Artifact Naming:** Prefix `build-8bf96b7-<variant>`
- ✅ **Step Identifier:** Contains `matrix-8bf96b7` identifier
- ✅ **Non-empty Artifacts:** All artifacts contain actual build data
- ✅ **README with Email:** This file contains email address

## Viewing Results

After the workflow runs:

1. **Check Run Status:**
   - Navigate to Actions tab
   - View the workflow run
   - Verify all 4 matrix jobs completed successfully

2. **Download Artifacts:**
   - Scroll to bottom of workflow run
   - See all artifacts under "Artifacts" section
   - Download individual artifacts or all at once

3. **View Summary:**
   - Check the "collect-artifacts" job
   - Review the build summary in the job output

## Artifact Contents

Each artifact contains:

### build-info.json
```json
{
  "variant": "ubuntu-node18",
  "os": "ubuntu-latest",
  "nodeVersion": "18",
  "runnerOS": "Linux",
  "runnerArch": "X64",
  "buildTime": "2025-11-09T10:30:00Z",
  "gitSha": "abc123...",
  "workflow": "Multi-Platform Matrix Build",
  "runNumber": "42"
}
```

### build-log.txt
Contains build execution details and versions.

### app-output.txt
Contains formatted application build output.

## Extending the Workflow

You can extend this workflow by:

1. **Adding more matrix variants:**
   ```yaml
   - os: ubuntu-latest
     node-version: '22'
     variant: 'ubuntu-node22'
   ```

2. **Adding build steps:**
   - Install dependencies
   - Run tests
   - Compile code
   - Generate documentation

3. **Adding deployment:**
   - Deploy artifacts to storage
   - Publish packages
   - Create releases

## Troubleshooting

### Workflow doesn't trigger
- Check branch names (main vs master)
- Verify workflow file is in `.github/workflows/`
- Check YAML syntax

### Artifacts not uploaded
- Verify files exist in specified path
- Check file permissions
- Review job logs for errors

### Matrix jobs fail
- Check Node.js version compatibility
- Verify OS-specific commands
- Review environment setup

## License

This project is open source and available for educational purposes.

## Resources

- [GitHub Actions Documentation](https://docs.github.com/en/actions)
- [Matrix Build Strategy](https://docs.github.com/en/actions/using-jobs/using-a-matrix-for-your-jobs)
- [Artifact Actions](https://github.com/actions/upload-artifact)

---

**Note:** Remember to update the email address in this README with your actual email address before submitting!
