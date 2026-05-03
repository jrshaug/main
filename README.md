# Law Firm Salesforce Template

This is the baseline template repository for all law firm Salesforce org projects. Every new law firm org repository is created from this template. It contains the standard folder structure, naming conventions, and base configuration that all projects build from.

---

## Table of Contents

- [Getting Started](#getting-started)
- [Repository Structure](#repository-structure)
- [Naming Conventions](#naming-conventions)
- [Branching Strategy](#branching-strategy)
- [Creating a New Org Repository](#creating-a-new-org-repository)
- [Developer Workflow](#developer-workflow)
- [Deploying to Salesforce](#deploying-to-salesforce)
- [Contributing to the Template](#contributing-to-the-template)
- [Contact](#contact)

---

## Getting Started

### Prerequisites

Make sure you have the following installed before you begin:

- [Visual Studio Code](https://code.visualstudio.com/)
- [Salesforce CLI](https://developer.salesforce.com/tools/salesforcecli)
- [Salesforce Extension Pack for VSCode](https://marketplace.visualstudio.com/items?itemName=salesforce.salesforcedx-vscode)
- [Git](https://git-scm.com/)
- GitHub account with access to the organization

### Verify your tools

```bash
sf --version
git --version
node --version
```

---

## Repository Structure

```
force-app/main/default/
├── lwc/                  # Lightning Web Components
├── classes/              # Apex classes
├── triggers/             # Apex triggers
├── objects/              # Custom objects and fields
├── permissionsets/       # Permission sets
├── flexipages/           # App and record pages
├── layouts/              # Page layouts
├── staticresources/      # Static files (images, CSS, JS)
└── tabs/                 # Custom tabs
config/                   # Org configuration and scratch org definition
scripts/                  # Utility and deploy scripts
.forceignore              # Files excluded from deploy/retrieve
sfdx-project.json         # Salesforce DX project configuration
README.md                 # You are here
```

---

## Naming Conventions

Consistent naming across all org repositories is critical. All developers must follow these conventions.

### Lightning Web Components (LWC)
- Use **camelCase**
- Be descriptive and specific
- Examples: `matterList`, `clientIntake`, `billingDashboard`, `documentViewer`

### Apex Classes
- Use **PascalCase**
- Suffix controllers with `Controller`, services with `Service`, utilities with `Util`
- Examples: `MatterController`, `BillingService`, `DocumentUtil`

### Apex Triggers
- Use **PascalCase**
- Name after the object they fire on, suffixed with `Trigger`
- Examples: `MatterTrigger`, `ContactTrigger`

### Custom Objects
- Use **Pascal_With_Underscores** ending in `__c`
- Examples: `Matter__c`, `Legal_Document__c`, `Billing_Entry__c`

### Custom Fields
- Use **Pascal_With_Underscores** ending in `__c`
- Examples: `Attorney_Name__c`, `Matter_Status__c`, `Billing_Rate__c`

### Permission Sets
- Use **ALL_CAPS_WITH_UNDERSCORES**
- Examples: `LAW_FIRM_ADMIN`, `ATTORNEY`, `PARALEGAL`, `STAFF`

### Branches
- Features: `feature/short-description`
- Bug fixes: `fix/short-description`
- Examples: `feature/matter-list-component`, `fix/billing-calculation-error`

---

## Branching Strategy

This project follows **GitHub Flow** — a simple, branch-based workflow.

```
main (always stable, always deployable)
  └── feature/your-feature-name
  └── fix/your-bug-fix-name
```

### Rules
- **Never commit directly to `main`**
- All changes must go through a **pull request**
- Pull requests require at least **one reviewer approval** before merging
- Delete your branch after it is merged
- Keep branches short-lived — a few hours to a few days

---

## Creating a New Org Repository

When onboarding a new law firm, follow these steps:

### Step 1: Create from template
1. Go to this repository on GitHub
2. Click **"Use this template"**
3. Click **"Create a new repository"**
4. Name it `org-firm-name` (example: `org-johnson-associates`)
5. Set visibility to **Private**
6. Click **"Create repository"**

### Step 2: Clone locally
```bash
git clone https://github.com/YOUR-ORG/org-firm-name.git
cd org-firm-name
```

### Step 3: Open in VSCode
```bash
code .
```

### Step 4: Authorize the org
```bash
# For sandbox
sf org login web --alias firm-sandbox --instance-url https://test.salesforce.com

# For production
sf org login web --alias firm-prod --instance-url https://login.salesforce.com
```

### Step 5: Set as default org
```bash
sf config set target-org firm-sandbox
```

---

## Developer Workflow

Follow these steps every time you work on a feature or fix.

### 1. Always start with the latest code
```bash
git checkout main
git pull origin main
```

### 2. Create a new branch
```bash
git checkout -b feature/your-feature-name
```

### 3. Make your changes in VSCode

### 4. Test in sandbox
```bash
sf project deploy start --metadata LightningComponentBundle:componentName --target-org firm-sandbox
```

### 5. Save your work with a commit
```bash
git add .
git commit -m "brief description of what you changed"
```

### 6. Push to GitHub
```bash
git push origin feature/your-feature-name
```

### 7. Open a Pull Request
1. Go to the repository on GitHub
2. Click **"Compare & pull request"**
3. Add a clear description of your changes
4. Request a reviewer
5. Wait for approval before merging

### 8. After merge — clean up
```bash
git checkout main
git pull origin main
git branch -d feature/your-feature-name
```

---

## Deploying to Salesforce

### Deploy a specific component
```bash
sf project deploy start --metadata LightningComponentBundle:componentName --target-org firm-prod
```

### Deploy all changes
```bash
sf project deploy start --source-dir force-app --target-org firm-prod
```

### Retrieve code from an org
```bash
sf project retrieve start --target-org firm-sandbox
```

### Check deployment status
```bash
sf project deploy report --use-most-recent
```

---

## Contributing to the Template

If you build something in an org repository that would benefit all law firms, it can be promoted to this template.

### Process
1. Identify the reusable component or pattern
2. Open a pull request in **this template repository**
3. Get approval from the template owner
4. Once merged, new org repositories created from this template will include it

### What belongs in the template
- Truly universal components used by every law firm
- Base utility classes
- Standard naming conventions and folder structure
- Shared configuration

### What does NOT belong in the template
- Firm-specific customizations
- Client-specific data or configuration
- One-off components built for a single firm

---

## Contact

For questions about this template, the development workflow, or onboarding a new firm:

- **Template Owner:** [Your Name]
- **GitHub Organization:** [Your GitHub Org URL]
- **Internal Contact:** [Team Slack channel or email]

---

*This template is maintained by the Salesforce Development Team.*
