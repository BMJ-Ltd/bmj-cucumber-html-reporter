# BMJ Cucumber HTML Reporter

Custom BMJ-branded HTML reporter for Cucumber test results in Cypress automation.

## Features

- 🎨 BMJ branding and styling with TailwindCSS
- 📊 Comprehensive test result visualization
- 🚀 Easy integration with Cypress and Cucumber preprocessor
- 📱 Responsive design

## Installation

### From GitHub (Recommended)

```bash
npm install github:BMJ-Ltd/bmj-cucumber-html-reporter#main
```

### From Local Development

```bash
npm install file:../path/to/bmj-cucumber-html-reporter
```

## Usage

```javascript
const report = require("bmj-cucumber-html-reporter");

report.generate({
  jsonDir: "./cypress/reports",
  reportPath: "./cypress/reports/index.html",
  pageTitle: "Cypress Test Report",
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
```

## Development

### Build

```bash
npm install
npm run build
```

This compiles TypeScript and generates TailwindCSS styles.

### Project Structure

```
bmj-cucumber-html-reporter/
├── src/
│   ├── generate-report.ts       # Main report generator
│   ├── templates/               # HTML templates with BMJ branding
│   │   ├── components/
│   │   ├── styles/
│   │   └── scripts/
│   └── types/                   # TypeScript definitions
├── dist/                        # Compiled output
├── package.json
└── tsconfig.json
```

## Requirements

- Node.js >= 18.x
- Cypress >= 13.x
- Cucumber preprocessor (@badeball/cypress-cucumber-preprocessor or cypress-cucumber-preprocessor)

## Credits

**Developed by:** Sandeep Kumar Patel (skpatel.bmj.com)  
**Team:** Platform Team  
**Organization:** BMJ Ltd  
**Version:** 1.0.0 (Beta)

Forked from [multiple-cucumber-html-reporter](https://github.com/WasiqB/multiple-cucumber-html-reporter) v3.10.0

## License

MIT
