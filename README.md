# BMJ Cucumber HTML Reporter

Custom BMJ-branded HTML reporter for Cucumber test results in Cypress automation.

[![Node Version](https://img.shields.io/badge/node-%3E%3D18.x-brightgreen.svg)](https://nodejs.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Cypress](https://img.shields.io/badge/cypress-%3E%3D13.x-brightgreen.svg)](https://www.cypress.io/)

---

## Table of Contents

- [Features](#features)
- [What's Included](#whats-included)
- [Installation](#installation)
  - [Prerequisites](#prerequisites)
  - [Install via GitHub](#install-via-github-recommended)
  - [Install from Specific Branch or Tag](#install-from-specific-branch-or-tag)
  - [Local Development Installation](#local-development-installation)
  - [Complete Local Development Workflow](#complete-local-development-workflow)
  - [Local Testing with Real Cypress Tests](#local-testing-with-real-cypress-tests)
  - [Debugging Local Changes](#debugging-local-changes)
  - [Quick Reference: Local Development Commands](#quick-reference-local-development-commands)
  - [Troubleshooting Local Setup](#troubleshooting-local-setup)
- [Usage](#usage)
  - [Quick Start](#quick-start)
  - [Configuration Options](#configuration-options)
  - [Advanced Examples](#advanced-examples)
  - [TypeScript Usage](#typescript-usage)
  - [Troubleshooting](#troubleshooting)
  - [Complete End-to-End Example](#complete-end-to-end-example)
- [Development](#development)
- [FAQ](#faq)
- [Contributing](#contributing)
- [Support](#support)
- [Credits](#credits)
- [License](#license)

## Features

- 🎨 **BMJ Branding** - Professional BMJ-styled reports with custom colors and branding
- 📊 **Rich Visualizations** - Interactive charts and graphs using ApexCharts
- 🔍 **Detailed Test Results** - View scenarios, steps, attachments, and error messages
- 📸 **Attachment Support** - Display screenshots, videos, and other attachments
- 📱 **Responsive Design** - Works perfectly on desktop, tablet, and mobile devices
- 🌓 **Dark Mode** - Toggle between light and dark themes
- 🔄 **Multiple Formats** - Support for various Cucumber JSON formats
- ⚡ **Fast & Lightweight** - Optimized performance with TailwindCSS
- 🎯 **Filter & Search** - Quickly find specific scenarios or features
- 📈 **Pass/Fail Metrics** - Clear overview of test execution statistics
- 🕐 **Duration Tracking** - Track execution time for features and scenarios
- 🏷️ **Tag Support** - Display and filter by Cucumber tags
- 📝 **Metadata Display** - Show browser, platform, device, and custom metadata
- 💾 **Export Options** - Generate standalone HTML reports for sharing

## What's Included

The generated HTML report includes:

- **Dashboard Summary** - Overview of total features, scenarios, steps, and pass/fail rates
- **Feature List** - Expandable list of all features with scenario details
- **Scenario Cards** - Detailed view of each scenario with:
  - Scenario status (passed, failed, skipped, etc.)
  - Individual step results
  - Error messages and stack traces
  - Embedded screenshots and videos
  - Step duration and timing information
- **Interactive Charts** - Visual representation of test results
- **Metadata Section** - Environment and execution details
- **Filtering Options** - Filter by status, tags, or feature names
- **Search Functionality** - Quick search across all scenarios
- **Theme Switcher** - Light/dark mode toggle

## Quick Example

```javascript
const report = require("bmj-cucumber-html-reporter");

report.generate({
  jsonDir: "./cypress/reports/cucumber-json",
  reportPath: "./cypress/reports/html/index.html",
  pageTitle: "My Test Report",
  reportName: "Test Results",
  displayDuration: true,
  metadata: {
    browser: { name: "chrome", version: "120" },
    platform: { name: "linux", version: "Ubuntu 22.04" }
  }
});
```

That's it! Your beautiful BMJ-branded HTML report will be generated at the specified path.

## Installation

> **Quick Install:** `npm install github:BMJ-Ltd/bmj-cucumber-html-reporter#main --save-dev`

### Installation Methods Comparison

| Method | Use Case | Command | Pros | Cons |
|--------|----------|---------|------|------|
| **GitHub** | Production use | `npm install github:BMJ-Ltd/...#main` | Latest stable, easy updates | Requires GitHub access |
| **Local Path** | Quick testing | `npm install file:../path/to/reporter` | Simple, isolated | Manual reinstall after changes |
| **npm link** | Active development | `npm link` | Changes reflect immediately | Requires rebuild |
| **package.json** | Team development | Add to dependencies | Version controlled | Path must be valid for all |

**Choose your method:**

- 🚀 **For CI/CD and Production:** Use GitHub installation
- 🔧 **For local development:** Use `npm link` 
- 🧪 **For quick testing:** Use `file:` path
- 👥 **For team collaboration:** Use `package.json` with relative path

### Prerequisites

- Node.js >= 18.x
- Cypress >= 13.x
- Cucumber preprocessor for Cypress:
  - [@badeball/cypress-cucumber-preprocessor](https://github.com/badeball/cypress-cucumber-preprocessor) (recommended)
  - OR [cypress-cucumber-preprocessor](https://github.com/TheBrainFamily/cypress-cucumber-preprocessor)

### Install via GitHub (Recommended)

```bash
npm install github:BMJ-Ltd/bmj-cucumber-html-reporter#main --save-dev
```

or with yarn:

```bash
yarn add github:BMJ-Ltd/bmj-cucumber-html-reporter#main --dev
```

### Install from Specific Branch or Tag

```bash
# Install from a specific branch
npm install github:BMJ-Ltd/bmj-cucumber-html-reporter#develop --save-dev

# Install from a specific tag/version
npm install github:BMJ-Ltd/bmj-cucumber-html-reporter#v1.0.0 --save-dev
```

### Local Development Installation

If you're developing or testing the reporter locally, there are multiple ways to use it.

#### Method 1: Install from Local Directory (Direct Path)

Install directly from a local directory path:

```bash
# From your test project directory
npm install file:../path/to/bmj-cucumber-html-reporter --save-dev

# Example with absolute path
npm install file:/home/user/projects/bmj-cucumber-html-reporter --save-dev

# Example with relative path
npm install file:../../bmj-cucumber-html-reporter --save-dev
```

**When to use:** Quick testing of the reporter in another project without making changes.

**Pros:** Simple, isolated installation  
**Cons:** Need to reinstall after every change to the reporter

#### Method 2: Using npm link (Recommended for Development)

Create a symbolic link to use the local version across multiple projects:

**Step 1: Link the reporter package**

```bash
# Navigate to the reporter directory
cd /path/to/bmj-cucumber-html-reporter

# Install dependencies and build
npm install
npm run build

# Create a global symlink
npm link
```

**Step 2: Link it in your test project**

```bash
# Navigate to your test project
cd /path/to/your-test-project

# Link to the local reporter
npm link bmj-cucumber-html-reporter
```

**Step 3: Make changes and rebuild**

```bash
# In the reporter directory, after making changes
cd /path/to/bmj-cucumber-html-reporter
npm run build

# Your test project will automatically use the updated version!
```

**Step 4: Unlink when done**

```bash
# In your test project
npm unlink bmj-cucumber-html-reporter

# In the reporter directory
npm unlink -g bmj-cucumber-html-reporter

# Reinstall from GitHub
npm install github:BMJ-Ltd/bmj-cucumber-html-reporter#main --save-dev
```

**When to use:** Active development, testing changes across multiple projects  
**Pros:** Changes reflect immediately after rebuild, no reinstallation needed  
**Cons:** Requires manual build after each change

#### Method 3: Using Relative Path in package.json

Add to your test project's `package.json`:

```json
{
  "dependencies": {
    "bmj-cucumber-html-reporter": "file:../bmj-cucumber-html-reporter"
  }
}
```

Then run:

```bash
npm install
```

**When to use:** Permanent local development setup  
**Pros:** Version controlled, team members can use same setup  
**Cons:** Path must be valid for all developers

### Complete Local Development Workflow

Here's a complete workflow for developing and testing the reporter locally:

```
┌─────────────────────────────────────────────────────────────────┐
│                    LOCAL DEVELOPMENT WORKFLOW                    │
└─────────────────────────────────────────────────────────────────┘

    Reporter Directory              Test Project Directory
    ══════════════════              ══════════════════════
    
    📁 bmj-cucumber-html-reporter   📁 my-test-project
    │                               │
    ├─ 1. Clone & Setup            ├─ 2. Create/Open Project
    │  └─ npm install              │  └─ npm init
    │                               │
    ├─ 3. Build                    ├─ 4. Link Reporter
    │  └─ npm run build            │  └─ npm link bmj-cucumber-html-reporter
    │                               │
    ├─ 5. Create Global Link       ├─ 6. Create Test Script
    │  └─ npm link                 │  └─ node test-report.js
    │                               │
    ├─ 7. Make Changes             │
    │  └─ Edit src/ files          │
    │                               │
    ├─ 8. Rebuild                  │
    │  └─ npm run build            │
    │                               │
    │                               └─ 9. Test Again
    │                                  └─ node test-report.js
    │                                     (Uses updated version!)
    └─ Repeat 7-9 as needed

```

**1. Clone and Setup the Reporter**

```bash
# Clone the repository
git clone https://github.com/BMJ-Ltd/bmj-cucumber-html-reporter.git
cd bmj-cucumber-html-reporter

# Install dependencies
npm install

# Build the project
npm run build

# Create global link (optional, for npm link method)
npm link
```

**2. Create a Test Project**

```bash
# Create a test directory
mkdir ~/test-reporter
cd ~/test-reporter

# Initialize npm
npm init -y

# Install Cypress and Cucumber (if testing with actual tests)
npm install --save-dev cypress @badeball/cypress-cucumber-preprocessor @bahmutov/cypress-esbuild-preprocessor

# Link to local reporter
npm link bmj-cucumber-html-reporter
# OR install from path
npm install file:../bmj-cucumber-html-reporter
```

**3. Create Test Data**

Create a sample Cucumber JSON file at `test-data/cucumber.json`:

```json
[
  {
    "description": "",
    "elements": [
      {
        "description": "",
        "id": "sample-feature;sample-scenario",
        "keyword": "Scenario",
        "line": 3,
        "name": "Sample Scenario",
        "steps": [
          {
            "keyword": "Given ",
            "line": 4,
            "name": "I have a precondition",
            "match": {
              "location": "step_definitions/steps.js:5"
            },
            "result": {
              "status": "passed",
              "duration": 1000000
            }
          },
          {
            "keyword": "When ",
            "line": 5,
            "name": "I perform an action",
            "match": {
              "location": "step_definitions/steps.js:10"
            },
            "result": {
              "status": "passed",
              "duration": 2000000
            }
          },
          {
            "keyword": "Then ",
            "line": 6,
            "name": "I should see the result",
            "match": {
              "location": "step_definitions/steps.js:15"
            },
            "result": {
              "status": "passed",
              "duration": 1500000
            }
          }
        ],
        "tags": [],
        "type": "scenario"
      }
    ],
    "id": "sample-feature",
    "keyword": "Feature",
    "line": 1,
    "name": "Sample Feature",
    "tags": [],
    "uri": "features/sample.feature"
  }
]
```

**4. Create Test Script**

Create `test-report.js`:

```javascript
const report = require("bmj-cucumber-html-reporter");
const path = require("path");

console.log("Generating report...");

try {
  report.generate({
    jsonDir: path.join(__dirname, "test-data"),
    reportPath: path.join(__dirname, "reports", "index.html"),
    pageTitle: "Local Test Report",
    reportName: "Development Test",
    displayDuration: true,
    displayReportTime: true,
    openReportInBrowser: true,
    metadata: {
      browser: {
        name: "chrome",
        version: "120"
      },
      device: "Local Machine",
      platform: {
        name: "linux",
        version: "Ubuntu 22.04"
      }
    },
    customData: {
      title: "Test Info",
      data: [
        { label: "Mode", value: "Local Development" },
        { label: "Tester", value: "Developer" }
      ]
    }
  });
  
  console.log("✅ Report generated successfully!");
  console.log("📄 Report location:", path.join(__dirname, "reports", "index.html"));
} catch (error) {
  console.error("❌ Error generating report:", error);
  process.exit(1);
}
```

**5. Run the Test**

```bash
node test-report.js
```

**6. Make Changes and Test**

```bash
# In the reporter directory, make your changes to src/ files
cd /path/to/bmj-cucumber-html-reporter

# Rebuild
npm run build

# Back to test project and run again
cd ~/test-reporter
node test-report.js
```

### Local Testing with Real Cypress Tests

If you want to test with actual Cypress tests:

**1. Setup Cypress in your test project**

```bash
cd ~/test-reporter

# Create Cypress structure
npx cypress open
# Close the window after it creates the structure

# Create feature file
mkdir -p cypress/e2e
```

**2. Create a simple feature** (`cypress/e2e/test.feature`)

```gherkin
Feature: Local Testing

  Scenario: Test the reporter
    Given I visit the homepage
    When I check the title
    Then I should see the correct title
```

**3. Create step definitions** (`cypress/support/step_definitions/steps.js`)

```javascript
import { Given, When, Then } from '@badeball/cypress-cucumber-preprocessor';

Given('I visit the homepage', () => {
  cy.visit('https://example.com');
});

When('I check the title', () => {
  cy.title().should('exist');
});

Then('I should see the correct title', () => {
  cy.title().should('include', 'Example');
});
```

**4. Configure Cypress** (`cypress.config.js`)

```javascript
import { defineConfig } from 'cypress';
import createBundler from '@bahmutov/cypress-esbuild-preprocessor';
import { addCucumberPreprocessorPlugin } from '@badeball/cypress-cucumber-preprocessor';
import { createEsbuildPlugin } from '@badeball/cypress-cucumber-preprocessor/esbuild';

export default defineConfig({
  e2e: {
    async setupNodeEvents(on, config) {
      await addCucumberPreprocessorPlugin(on, config);
      
      on(
        'file:preprocessor',
        createBundler({
          plugins: [createEsbuildPlugin(config)],
        })
      );
      
      return config;
    },
    specPattern: 'cypress/e2e/**/*.feature',
  },
});
```

**5. Configure Cucumber preprocessor** (`.cypress-cucumber-preprocessorrc.json`)

```json
{
  "json": {
    "enabled": true,
    "output": "cypress/reports/cucumber-json/report.json"
  }
}
```

**6. Update package.json**

```json
{
  "scripts": {
    "test": "cypress run",
    "report": "node test-report.js",
    "test:report": "cypress run && node test-report.js"
  }
}
```

**7. Update test-report.js**

```javascript
const report = require("bmj-cucumber-html-reporter");

report.generate({
  jsonDir: "./cypress/reports/cucumber-json",
  reportPath: "./cypress/reports/html/index.html",
  pageTitle: "Local Test Report",
  reportName: "Cypress Test Results",
  displayDuration: true,
  openReportInBrowser: true
});
```

**8. Run tests and generate report**

```bash
npm run test:report
```

### Debugging Local Changes

When developing locally, you can add debug logging:

```javascript
// In your test script
const report = require("bmj-cucumber-html-reporter");

console.log("Reporter version:", require("bmj-cucumber-html-reporter/package.json").version);
console.log("Reporter path:", require.resolve("bmj-cucumber-html-reporter"));

report.generate({
  jsonDir: "./test-data",
  reportPath: "./reports/index.html",
  disableLog: false  // Enable logging
});
```

### Quick Reference: Local Development Commands

**Initial Setup**
```bash
# In reporter directory
cd /path/to/bmj-cucumber-html-reporter
npm install                    # Install dependencies
npm run build                  # Build the project
npm link                       # Create global link

# In test project directory
cd /path/to/test-project
npm link bmj-cucumber-html-reporter  # Link to local reporter
```

**Development Cycle**
```bash
# Make changes in reporter
cd /path/to/bmj-cucumber-html-reporter
# Edit files in src/
npm run build                  # Rebuild after changes

# Test in your project
cd /path/to/test-project
node test-report.js           # Run your test script
```

**Common Commands**
```bash
# Check if linked correctly
npm list bmj-cucumber-html-reporter

# View current version
npm list bmj-cucumber-html-reporter --depth=0

# Rebuild CSS and TypeScript
npm run build

# Rebuild CSS only
npm run generate:css

# Unlink and reinstall from GitHub
npm unlink bmj-cucumber-html-reporter
npm install github:BMJ-Ltd/bmj-cucumber-html-reporter#main --save-dev

# Clear and reinstall
npm cache clean --force
rm -rf node_modules package-lock.json
npm install
```

**Debugging**
```bash
# Check where module is loading from
node -e "console.log(require.resolve('bmj-cucumber-html-reporter'))"

# List all globally linked packages
npm ls -g --depth=0 --link=true

# Verify build output
ls -la /path/to/bmj-cucumber-html-reporter/lib/

# Watch for file changes (requires nodemon)
npm install -g nodemon
nodemon --watch src --exec "npm run build"
```

### Troubleshooting Local Setup

**Issue: Changes not reflecting**

```bash
# Make sure you rebuild after changes
cd /path/to/bmj-cucumber-html-reporter
npm run build

# Verify the build succeeded
ls -la lib/
```

**Issue: Module not found**

```bash
# Check if link exists
npm list bmj-cucumber-html-reporter

# Recreate the link
npm unlink bmj-cucumber-html-reporter
cd /path/to/bmj-cucumber-html-reporter
npm link
cd /path/to/test-project
npm link bmj-cucumber-html-reporter
```

**Issue: Using old version**

```bash
# Clear npm cache
npm cache clean --force

# Reinstall
npm unlink bmj-cucumber-html-reporter
npm install file:/path/to/bmj-cucumber-html-reporter
```

### Verify Installation

```bash
npm list bmj-cucumber-html-reporter
```

## Usage

### Quick Start

#### 1. Install the package

```bash
npm install github:BMJ-Ltd/bmj-cucumber-html-reporter#main --save-dev
```

#### 2. Generate Cucumber JSON reports in your Cypress tests

Ensure your Cypress Cucumber preprocessor is configured to generate JSON reports:

```javascript
// cypress.config.js or cypress.config.ts
import { defineConfig } from 'cypress';
import createBundler from '@bahmutov/cypress-esbuild-preprocessor';
import { addCucumberPreprocessorPlugin } from '@badeball/cypress-cucumber-preprocessor';
import { createEsbuildPlugin } from '@badeball/cypress-cucumber-preprocessor/esbuild';

export default defineConfig({
  e2e: {
    async setupNodeEvents(on, config) {
      await addCucumberPreprocessorPlugin(on, config);
      
      on(
        'file:preprocessor',
        createBundler({
          plugins: [createEsbuildPlugin(config)],
        })
      );
      
      return config;
    },
    specPattern: 'cypress/e2e/**/*.feature',
  },
});
```

Configure the preprocessor to output JSON:

```json
// .cypress-cucumber-preprocessorrc.json
{
  "json": {
    "enabled": true,
    "output": "cypress/reports/cucumber-json/report.json"
  }
}
```

#### 3. Create a report generation script

Create a file `generate-report.js` in your project root:

```javascript
const report = require("bmj-cucumber-html-reporter");

report.generate({
  jsonDir: "./cypress/reports/cucumber-json",
  reportPath: "./cypress/reports/html/index.html",
  pageTitle: "BMJ Test Report",
  reportName: "Test Execution Results",
  displayDuration: true,
  displayReportTime: true,
  metadata: {
    browser: {
      name: "chrome",
      version: "120"
    },
    device: "Local Machine",
    platform: {
      name: "linux",
      version: "Ubuntu 22.04"
    }
  }
});

console.log("Report generated successfully!");
```

#### 4. Add npm script to your package.json

```json
{
  "scripts": {
    "cypress:run": "cypress run",
    "report:generate": "node generate-report.js",
    "test": "npm run cypress:run && npm run report:generate"
  }
}
```

#### 5. Run your tests and generate report

```bash
npm test
```

The HTML report will be generated at `./cypress/reports/html/index.html`

### Configuration Options

All available configuration options:

```javascript
report.generate({
  // Required options
  jsonDir: "./cypress/reports/cucumber-json",      // Directory containing Cucumber JSON files
  reportPath: "./cypress/reports/html/index.html", // Output path for HTML report
  
  // Report customization
  pageTitle: "BMJ Test Report",                    // Browser tab title
  reportName: "Test Execution Results",            // Report header title
  pageFooter: "<div>Custom footer content</div>",  // Custom HTML footer (null to hide)
  
  // Display options
  displayDuration: true,                           // Show test duration
  displayReportTime: true,                         // Show report generation time
  durationInMS: false,                             // Display duration in milliseconds (default: seconds)
  durationAggregation: 'wallClock',               // 'wallClock' or 'sum'
  hideMetadata: false,                             // Hide metadata section
  
  // Styling options
  customStyle: "./path/to/custom.css",            // Path to custom CSS file
  overrideStyle: "./path/to/override.css",        // Path to CSS file that overrides default styles
  
  // Metadata (browser, device, platform info)
  metadata: {
    browser: {
      name: "chrome",
      version: "120"
    },
    device: "Local Machine",
    platform: {
      name: "linux",
      version: "Ubuntu 22.04"
    },
    app: {
      name: "BMJ Masterclasses",
      version: "1.0.0"
    }
  },
  
  // Custom metadata format (alternative to object format)
  customMetadata: false,                          // Use array format for metadata
  
  // Custom data section
  customData: {
    title: "Test Run Info",
    data: [
      { label: "Project", value: "BMJ Masterclasses" },
      { label: "Environment", value: "Staging" },
      { label: "Build", value: "1.2.3" },
      { label: "Branch", value: "main" }
    ]
  },
  
  // Advanced options
  saveCollectedJSON: false,                       // Save collected JSON data to file
  openReportInBrowser: true,                      // Automatically open report in browser
  disableLog: false,                              // Disable console logging
  plainDescription: false,                        // Render descriptions as plain text
  useCDN: false,                                  // Use CDN for external libraries
  staticFilePath: false                           // Use relative paths for static files
});
```

### Advanced Examples

#### Example 1: Minimal Configuration

```javascript
const report = require("bmj-cucumber-html-reporter");

report.generate({
  jsonDir: "./cypress/reports/cucumber-json",
  reportPath: "./cypress/reports/html/index.html"
});
```

#### Example 2: With Custom Styling

```javascript
const report = require("bmj-cucumber-html-reporter");

report.generate({
  jsonDir: "./cypress/reports/cucumber-json",
  reportPath: "./cypress/reports/html/index.html",
  pageTitle: "BMJ Masterclasses Test Report",
  reportName: "Regression Test Suite",
  customStyle: "./custom-styles/theme.css",
  displayDuration: true,
  displayReportTime: true
});
```

#### Example 3: CI/CD Integration

```javascript
const report = require("bmj-cucumber-html-reporter");

report.generate({
  jsonDir: "./cypress/reports/cucumber-json",
  reportPath: "./cypress/reports/html/index.html",
  pageTitle: `Test Report - Build #${process.env.BUILD_NUMBER}`,
  reportName: "Automated Test Execution",
  displayDuration: true,
  displayReportTime: true,
  durationInMS: true,
  openReportInBrowser: false, // Don't open in CI
  metadata: {
    browser: {
      name: process.env.BROWSER || "chrome",
      version: process.env.BROWSER_VERSION || "latest"
    },
    device: "CI Runner",
    platform: {
      name: process.env.PLATFORM || "linux",
      version: process.env.PLATFORM_VERSION || "Ubuntu 22.04"
    }
  },
  customData: {
    title: "CI/CD Info",
    data: [
      { label: "Build Number", value: process.env.BUILD_NUMBER || "N/A" },
      { label: "Branch", value: process.env.GIT_BRANCH || "N/A" },
      { label: "Commit", value: process.env.GIT_COMMIT || "N/A" },
      { label: "Environment", value: process.env.TEST_ENV || "staging" }
    ]
  }
});
```

#### Example 4: Multiple Test Suites

```javascript
const report = require("bmj-cucumber-html-reporter");
const path = require("path");

// Generate separate reports for different test suites
const suites = ["smoke", "regression", "integration"];

suites.forEach(suite => {
  report.generate({
    jsonDir: path.join("./cypress/reports/cucumber-json", suite),
    reportPath: path.join("./cypress/reports/html", suite, "index.html"),
    pageTitle: `${suite.toUpperCase()} Test Report`,
    reportName: `${suite.charAt(0).toUpperCase() + suite.slice(1)} Tests`,
    displayDuration: true,
    displayReportTime: true,
    customData: {
      title: "Suite Info",
      data: [
        { label: "Suite", value: suite },
        { label: "Date", value: new Date().toISOString() }
      ]
    }
  });
});
```

### TypeScript Usage

```typescript
import * as report from "bmj-cucumber-html-reporter";
import type { Options } from "bmj-cucumber-html-reporter";

const options: Options = {
  jsonDir: "./cypress/reports/cucumber-json",
  reportPath: "./cypress/reports/html/index.html",
  pageTitle: "BMJ Test Report",
  reportName: "Test Execution Results",
  displayDuration: true,
  displayReportTime: true,
  metadata: {
    browser: {
      name: "chrome",
      version: "120"
    },
    device: "Local Machine",
    platform: {
      name: "linux",
      version: "Ubuntu 22.04"
    }
  }
};

report.generate(options);
```

### Troubleshooting

#### No JSON files found

Ensure your Cucumber preprocessor is configured to output JSON files:

```json
// .cypress-cucumber-preprocessorrc.json
{
  "json": {
    "enabled": true,
    "output": "cypress/reports/cucumber-json/report.json"
  }
}
```

#### Report not generating

Check that:
1. The `jsonDir` path contains valid Cucumber JSON files
2. The output directory in `reportPath` exists or can be created
3. You have write permissions to the output directory

#### Custom styles not applying

Make sure:
1. The CSS file path is correct and accessible
2. Use `customStyle` to add styles, `overrideStyle` to override defaults
3. CSS selectors target the correct elements in the generated HTML

## Development

### Setup Development Environment

```bash
# Clone the repository
git clone https://github.com/BMJ-Ltd/bmj-cucumber-html-reporter.git
cd bmj-cucumber-html-reporter

# Install dependencies
npm install
```

### Build

```bash
# Full build (includes CSS generation and TypeScript compilation)
npm run build
```

This will:
1. Generate TailwindCSS styles (regular and minified)
2. Compile TypeScript files to JavaScript
3. Copy template files to the `lib` directory

### Available Scripts

```bash
# Generate CSS (development)
npm run generate:css

# Generate minified CSS (production)
npm run generate:css:min

# Build TypeScript and templates
npm run build

# Prepare for publishing (runs build automatically)
npm run prepare
```

### Project Structure

```
bmj-cucumber-html-reporter/
├── src/                          # Source files
│   ├── generate-report.ts        # Main report generator
│   ├── collect-jsons.ts          # JSON collection utility
│   ├── types.ts                  # TypeScript type definitions
│   ├── templates/                # Liquid templates and assets
│   │   ├── layout.liquid         # Main layout template
│   │   ├── index.liquid          # Dashboard template
│   │   ├── feature.liquid        # Feature detail template
│   │   ├── includes/             # Reusable template components
│   │   ├── scripts/              # Client-side JavaScript
│   │   ├── styles/               # TailwindCSS styles
│   │   └── assets/               # Generated CSS, fonts, etc.
│   └── test/                     # Test files
├── lib/                          # Compiled output (generated)
├── package.json                  # Package configuration
├── tsconfig.json                 # TypeScript configuration
└── README.md                     # This file
```

### Making Changes

1. **Modify TypeScript files** in `src/`
2. **Update templates** in `src/templates/`
3. **Modify styles** in `src/templates/styles/main.css`
4. **Run build** to compile: `npm run build`
5. **Test locally** by installing in another project:
   ```bash
   npm install file:../path/to/bmj-cucumber-html-reporter
   ```

### Testing Changes

```bash
# Run tests (if available)
npm test

# Test the report generation locally
node src/test/test.ts
```

### Publishing

```bash
# Build the project
npm run build

# Commit your changes
git add .
git commit -m "Your commit message"
git push origin main

# Create a tag for versioning
git tag v1.0.1
git push origin v1.0.1
```

Users can then install the specific version:
```bash
npm install github:BMJ-Ltd/bmj-cucumber-html-reporter#v1.0.1 --save-dev
```

## FAQ

### Q: Where should I place the Cucumber JSON files?

**A:** You can place them anywhere, but typically `cypress/reports/cucumber-json/` is recommended. Configure this in your `.cypress-cucumber-preprocessorrc.json`:

```json
{
  "json": {
    "enabled": true,
    "output": "cypress/reports/cucumber-json/report.json"
  }
}
```

### Q: Can I use this with other testing frameworks besides Cypress?

**A:** Yes! This reporter works with any tool that generates Cucumber JSON format. Just point the `jsonDir` to your JSON output directory.

### Q: How do I add screenshots to the report?

**A:** Screenshots are automatically included if your Cucumber JSON contains attachments. In Cypress:

```javascript
// In your step definitions
cy.screenshot('scenario-name');
```

The preprocessor will automatically include these in the JSON output.

### Q: Can I customize the report styling?

**A:** Yes! Use the `customStyle` option to add your own CSS:

```javascript
report.generate({
  jsonDir: "./cypress/reports/cucumber-json",
  reportPath: "./cypress/reports/html/index.html",
  customStyle: "./my-custom-styles.css"
});
```

### Q: How do I generate reports in CI/CD?

**A:** Add the report generation as a post-test step:

```yaml
# Example GitHub Actions
- name: Run Cypress tests
  run: npm run cypress:run

- name: Generate HTML report
  if: always()
  run: npm run report:generate

- name: Upload report
  if: always()
  uses: actions/upload-artifact@v3
  with:
    name: test-report
    path: cypress/reports/html/
```

### Q: The report shows "No features found"

**A:** This means no valid Cucumber JSON files were found in the `jsonDir`. Check:
1. JSON files are present in the specified directory
2. JSON files are valid Cucumber format
3. The path is correct (relative to where you run the script)

### Q: Can I generate multiple reports?

**A:** Yes! You can call `report.generate()` multiple times with different configurations:

```javascript
// Smoke tests report
report.generate({
  jsonDir: "./reports/smoke",
  reportPath: "./reports/html/smoke/index.html",
  pageTitle: "Smoke Tests"
});

// Regression tests report
report.generate({
  jsonDir: "./reports/regression",
  reportPath: "./reports/html/regression/index.html",
  pageTitle: "Regression Tests"
});
```

### Complete End-to-End Example

Here's a complete example showing the entire workflow from setup to report generation:

**Step 1: Project Setup**

```bash
# Initialize a new project
npm init -y

# Install Cypress and Cucumber
npm install --save-dev cypress @badeball/cypress-cucumber-preprocessor @bahmutov/cypress-esbuild-preprocessor

# Install the reporter
npm install --save-dev github:BMJ-Ltd/bmj-cucumber-html-reporter#main
```

**Step 2: Configure Cypress** (`cypress.config.js`)

```javascript
import { defineConfig } from 'cypress';
import createBundler from '@bahmutov/cypress-esbuild-preprocessor';
import { addCucumberPreprocessorPlugin } from '@badeball/cypress-cucumber-preprocessor';
import { createEsbuildPlugin } from '@badeball/cypress-cucumber-preprocessor/esbuild';

export default defineConfig({
  e2e: {
    async setupNodeEvents(on, config) {
      await addCucumberPreprocessorPlugin(on, config);
      
      on(
        'file:preprocessor',
        createBundler({
          plugins: [createEsbuildPlugin(config)],
        })
      );
      
      return config;
    },
    specPattern: 'cypress/e2e/**/*.feature',
    supportFile: 'cypress/support/e2e.js'
  },
});
```

**Step 3: Configure Cucumber Preprocessor** (`.cypress-cucumber-preprocessorrc.json`)

```json
{
  "json": {
    "enabled": true,
    "output": "cypress/reports/cucumber-json/report-[datetime].json",
    "formatter": "cucumber-json-formatter"
  },
  "stepDefinitions": [
    "cypress/e2e/**/*.{js,ts}",
    "cypress/support/step_definitions/**/*.{js,ts}"
  ]
}
```

**Step 4: Create a Feature File** (`cypress/e2e/login.feature`)

```gherkin
Feature: User Login

  Scenario: Successful login with valid credentials
    Given I am on the login page
    When I enter valid credentials
    And I click the login button
    Then I should be redirected to the dashboard
    And I should see a welcome message

  Scenario: Failed login with invalid credentials
    Given I am on the login page
    When I enter invalid credentials
    And I click the login button
    Then I should see an error message
    And I should remain on the login page
```

**Step 5: Create Step Definitions** (`cypress/support/step_definitions/login.js`)

```javascript
import { Given, When, Then } from '@badeball/cypress-cucumber-preprocessor';

Given('I am on the login page', () => {
  cy.visit('/login');
});

When('I enter valid credentials', () => {
  cy.get('#username').type('testuser');
  cy.get('#password').type('password123');
});

When('I enter invalid credentials', () => {
  cy.get('#username').type('wronguser');
  cy.get('#password').type('wrongpass');
});

When('I click the login button', () => {
  cy.get('#login-btn').click();
});

Then('I should be redirected to the dashboard', () => {
  cy.url().should('include', '/dashboard');
});

Then('I should see a welcome message', () => {
  cy.contains('Welcome').should('be.visible');
  cy.screenshot('successful-login');
});

Then('I should see an error message', () => {
  cy.contains('Invalid credentials').should('be.visible');
  cy.screenshot('failed-login');
});

Then('I should remain on the login page', () => {
  cy.url().should('include', '/login');
});
```

**Step 6: Create Report Generator** (`generate-report.js`)

```javascript
const report = require("bmj-cucumber-html-reporter");
const os = require("os");

report.generate({
  jsonDir: "./cypress/reports/cucumber-json",
  reportPath: "./cypress/reports/html/index.html",
  pageTitle: "BMJ Test Report",
  reportName: "Login Feature Test Results",
  displayDuration: true,
  displayReportTime: true,
  durationInMS: false,
  openReportInBrowser: true,
  metadata: {
    browser: {
      name: "chrome",
      version: "120"
    },
    device: os.hostname(),
    platform: {
      name: os.platform(),
      version: os.release()
    }
  },
  customData: {
    title: "Test Environment",
    data: [
      { label: "Project", value: "BMJ Masterclasses" },
      { label: "Environment", value: "Staging" },
      { label: "Executed By", value: os.userInfo().username },
      { label: "Date", value: new Date().toLocaleString() }
    ]
  }
});

console.log("✅ Report generated successfully!");
```

**Step 7: Update package.json**

```json
{
  "scripts": {
    "cy:open": "cypress open",
    "cy:run": "cypress run",
    "report:generate": "node generate-report.js",
    "test": "cypress run && node generate-report.js",
    "test:headed": "cypress run --headed && node generate-report.js"
  }
}
```

**Step 8: Run Tests and Generate Report**

```bash
# Run tests and generate report
npm test

# Or run in headed mode
npm run test:headed

# Or open Cypress UI
npm run cy:open
```

The HTML report will be automatically opened in your browser at `cypress/reports/html/index.html`.

## Contributing

We welcome contributions! To contribute:

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/my-new-feature`
3. Make your changes
4. Run the build: `npm run build`
5. Commit your changes: `git commit -am 'Add some feature'`
6. Push to the branch: `git push origin feature/my-new-feature`
7. Submit a pull request

### Contribution Guidelines

- Follow the existing code style
- Add tests for new features
- Update documentation as needed
- Ensure all tests pass before submitting PR
- Keep commits atomic and well-described

## Support

### Getting Help

If you encounter issues or have questions:

1. **Check the [FAQ](#faq)** - Common questions and solutions
2. **Review [Troubleshooting](#troubleshooting)** - Common issues and fixes
3. **Check existing issues** - Someone may have already reported it
4. **Create a new issue** - Provide detailed information:
   - Version of bmj-cucumber-html-reporter
   - Node.js and Cypress versions
   - Error messages and stack traces
   - Sample JSON file (if relevant)
   - Steps to reproduce

### Reporting Bugs

When reporting bugs, please include:

- Clear description of the issue
- Steps to reproduce
- Expected vs actual behavior
- Environment details (OS, Node version, etc.)
- Sample code or JSON files if possible
- Screenshots of the issue (if applicable)

### Feature Requests

We welcome feature requests! Please:

- Check if the feature already exists
- Clearly describe the use case
- Explain why it would be valuable
- Provide examples if possible

### Contact

- **Developer:** Sandeep Kumar Patel (skpatel.bmj.com)
- **Team:** Platform Team, BMJ Ltd
- **Repository:** [GitHub](https://github.com/BMJ-Ltd/bmj-cucumber-html-reporter)

## Credits

**Developed by:** Sandeep Kumar Patel (skpatel.bmj.com)  
**Team:** Platform Team  
**Organization:** BMJ Ltd  
**Version:** 1.0.0 (Beta)

Forked from [multiple-cucumber-html-reporter](https://github.com/WasiqB/multiple-cucumber-html-reporter) v3.10.0

## License

MIT
