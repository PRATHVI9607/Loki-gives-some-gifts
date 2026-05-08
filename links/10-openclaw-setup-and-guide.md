# OpenClaw - Complete Setup & User Guide

## Table of Contents
1. [Installation & Setup](#installation--setup)
2. [Getting Started](#getting-started)
3. [Model Configuration](#model-configuration)
4. [Features & Capabilities](#features--capabilities)
5. [Workflows & Best Practices](#workflows--best-practices)
6. [Skills & Tools](#skills--tools)
7. [Advanced Usage](#advanced-usage)
8. [Troubleshooting](#troubleshooting)

## Installation & Setup

### Prerequisites
- Python 3.9+
- Docker (recommended)
- PostgreSQL 12+ (for data persistence)
- 2GB+ available disk space
- API credentials

### Installation Methods

#### Method 1: Docker (Recommended)
```bash
# Pull latest image
docker pull openclaw:latest

# Run container
docker run -d \
  --name openclaw \
  -e OPENCLAW_API_KEY=your_key \
  -e OPENCLAW_MODEL=claude-3-5-sonnet \
  -p 8080:8080 \
  openclaw:latest
```

#### Method 2: Local Installation
```bash
# Clone repository
git clone https://github.com/openclaw/openclaw.git
cd openclaw

# Install dependencies
pip install -e .

# Initialize database
openclaw db init

# Start service
openclaw server start
```

### Initial Configuration
```bash
# Configure API credentials
openclaw config set api-key YOUR_API_KEY

# Set default model
openclaw config set model claude-3-5-sonnet

# Enable features
openclaw config set features.caching true
openclaw config set features.logging true
```

## User Interface & Dashboard

### Web Dashboard Access
Web UI available at `http://localhost:8080`

#### Main Dashboard Components
```
┌─────────────────────────────────────────────┐
│ OpenClaw Dashboard                          │
├─────────────────────────────────────────────┤
│ Home │ Projects │ Analysis │ Reports │ Team │
├─────────────────────────────────────────────┤
│ ┌─────────────┐  ┌──────────────────────┐  │
│ │ Code Health │  │ Recent Issues        │  │
│ │ Score: 87%  │  │ ├─ Security: 3      │  │
│ └─────────────┘  │ ├─ Performance: 5   │  │
│                  │ └─ Quality: 2       │  │
│ ┌─────────────┐  ├──────────────────────┤  │
│ │ Test Cvg:   │  │ Team Activity        │  │
│ │ 82%         │  │ • John: Fixed issue  │  │
│ └─────────────┘  │ • Sarah: +10% cov    │  │
└─────────────────────────────────────────────┘
```

#### Dashboard Features
- **Real-time Metrics**: Live code quality scores
- **Issue Tracking**: Categorized by type/severity
- **Team Insights**: Contributor activity
- **Trend Analysis**: Historical metrics visualization
- **Custom Reports**: Export and share
- **Notifications Panel**: Real-time alerts

#### Web UI Workflows
```
Analyze Code:
1. Dashboard → Projects → Select Project
2. Click "Scan Now" button
3. Monitor progress in real-time
4. View results dashboard
5. Click issues for details

Code Review:
1. Dashboard → Pull Requests
2. Select PR from list
3. View diff highlighting
4. Add inline comments
5. Generate review summary

Team Collaboration:
1. Dashboard → Team
2. Invite members
3. Assign issues
4. Comment on findings
5. Track assignments
```

### Terminal UI (TUI) Interface
Start interactive TUI:
```bash
openclaw tui
```

#### TUI Main Menu
```
╔═══════════════════════════════════════════╗
║        OpenClaw - Terminal UI             ║
╠═══════════════════════════════════════════╣
║                                           ║
║  [1] Projects                             ║
║  [2] Quick Scan                           ║
║  [3] Analysis Results                     ║
║  [4] Reports                              ║
║  [5] Settings                             ║
║  [6] Help                                 ║
║  [Q] Quit                                 ║
║                                           ║
║  Enter selection or type command:         ║
║  >_                                       ║
║                                           ║
╚═══════════════════════════════════════════╝
```

#### TUI Command Reference
```
Basic Navigation:
  1/2/3...    → Select menu item
  q/Q         → Quit current view
  ?           → Show help
  :/cmd       → Execute command
  Ctrl+C      → Go back

Project Management:
  projects        → List all projects
  projects create → New project
  projects scan   → Scan current project
  projects rm     → Delete project

Analysis Commands:
  scan          → Analyze codebase
  scan fast     → Quick scan (Haiku)
  scan deep     → Deep scan (Opus)
  scan --file   → Scan specific file
  results       → Show analysis results
  issues        → List all issues
  issues HIGH   → Show high severity only

Filtering & Search:
  /keyword      → Search issues
  filter type   → By issue type
  filter file   → By file name
  sort name     → Sort results

Reporting:
  report         → Generate report
  export json    → Export as JSON
  export md      → Export as Markdown
  export pdf     → Export as PDF

Settings:
  set model          → Change AI model
  set theme          → Change TUI theme
  set columns        → Adjust display
  config show        → View settings
```

#### TUI Display Modes
```bash
# List view (default)
openclaw tui --view list

# Table view
openclaw tui --view table

# Tree view (hierarchical)
openclaw tui --view tree

# Graph view (dependency graph)
openclaw tui --view graph
```

#### TUI Color Themes
```bash
openclaw tui --theme dark
openclaw tui --theme light
openclaw tui --theme monokai
openclaw tui --theme nord
openclaw tui --theme dracula
```

#### TUI Keyboard Shortcuts
```
Navigation:
  ↑/↓         → Move cursor
  Page Up/Dn  → Scroll page
  Home/End    → Jump to edges
  f/F         → Forward search
  n/N         → Next/Previous match

Selection & Actions:
  Space       → Toggle selection
  Shift+Space → Select all
  Ctrl+A      → Select all
  d           → Delete/Dismiss
  e           → Expand/Edit
  v           → View details
  c           → Copy to clipboard

Special:
  :           → Command mode
  /           → Search mode
  Ctrl+L      → Clear screen
  Ctrl+R      → Refresh
  Ctrl+S      → Save/Export
```

### Docker/Web API Interface

#### REST API Endpoints
```bash
# Analyze code
POST /api/v1/analyze
Body: {"projectId": "123", "path": "./src"}

# Get results
GET /api/v1/results/:analysisId

# List projects
GET /api/v1/projects

# Create project
POST /api/v1/projects
Body: {"name": "myproject", "type": "python"}

# Get metrics
GET /api/v1/projects/:id/metrics

# List issues
GET /api/v1/projects/:id/issues?severity=HIGH
```

#### WebSocket Real-time Updates
```javascript
// Connect to live analysis
const ws = new WebSocket('ws://localhost:8080/api/v1/live');

ws.on('message', (data) => {
  // Real-time analysis progress
  // Issue discoveries
  // Completion status
});
```
```bash
# Verify installation
openclaw --version

# Run first analysis
openclaw analyze "Fix this code: function add(a,b) { return a + b; }"

# Check status
openclaw status
```

### Project Setup - Via Web UI
```
Dashboard → Projects → New Project

1. Enter project name
2. Select programming language
3. Configure code source:
   - Upload files
   - Git repository
   - Connected workspace
4. Select framework (optional)
5. Configure dependencies
6. Click "Create Project"
```

### Basic Commands
```bash
# Run analysis on codebase
openclaw scan ./src

# Check code quality
openclaw quality-check ./src

# Generate insights
openclaw insights ./src --output report.json
```

## Model Configuration

### Available Models
- **claude-3-5-sonnet**: Production default (fast, accurate)
- **claude-3-opus**: Deep analysis (slower, comprehensive)
- **claude-3-haiku**: Quick analysis (fastest, lightweight)

### Switch Models via UI
```
Web Dashboard:
1. Settings → Model Selection
2. Choose from dropdown
3. See performance estimate
4. Click Apply

TUI:
1. Press : to enter command mode
2. Type: set model claude-3-opus
3. Press Enter
4. Changes apply immediately

API:
POST /api/v1/config/model
Body: {"model": "claude-3-opus"}
```

### Fine-Tuning Parameters
```yaml
# openclaw.yml
models:
  default: claude-3-5-sonnet
  fallback: claude-3-haiku
  parameters:
    temperature: 0.5
    max_tokens: 2048
    top_p: 0.95
    frequency_penalty: 0.2
```

### Model Selection Strategy
```
├── Quick Prototyping → Haiku
├── Feature Development → Sonnet
├── Critical Analysis → Opus
└── Hybrid Approach → Auto-select
```

## Features & Capabilities

### Core Analysis Features
- **Static Analysis**: Code patterns, antipatterns, bugs
- **Dynamic Analysis**: Runtime behavior prediction
- **Security Scanning**: Vulnerability detection
- **Performance Analysis**: Optimization opportunities
- **Complexity Metrics**: Maintainability scoring

### Generation Features
- **Code Generation**: From descriptions or patterns
- **Test Generation**: Unit, integration, e2e tests
- **Documentation**: Auto-generated docs with examples
- **Refactoring Suggestions**: Code improvements
- **Architecture Recommendations**: System design

### Integration Features
- **Git Integration**: Diff analysis, commit hooks
- **CI/CD Integration**: GitHub Actions, GitLab CI, Jenkins
- **IDE Integration**: VS Code, JetBrains IDEs
- **Monitoring**: Analytics dashboard, reporting
- **Webhooks**: Event-driven automation

### Collaborative Features
- **Team Projects**: Shared analysis
- **Code Review Integration**: Inline suggestions
- **Comment Threads**: Team discussions
- **Role-Based Access**: Permission management
- **Audit Logging**: Change tracking

## Advanced UI Features

### Web Dashboard Advanced Usage

#### Custom Dashboards
```
Dashboard → Customize

• Drag-drop widgets
• Add/remove panels
• Save custom layout
• Share with team
• Set as default
```

#### Collaboration Features
```
Right-click Issue:
  • Add Comment
  • @Mention Team
  • Assign To
  • Link Issue
  • Status Change
  • Priority Update
  • Due Date Set
  • Subscribe/Notify
```

#### Metrics Visualization
```
• Line charts: Historical trends
• Bar charts: Comparisons
• Pie charts: Distributions
• Heatmaps: Coverage maps
• Scatter plots: Correlations
• Custom visualizations
```

#### Export & Sharing
```
Dashboard → Export:

• PDF Reports
• JSON Data
• Markdown Docs
• HTML Pages
• CSV Tables
• Custom Templates

Share:
• Generate public link
• Email report
• Slack integration
• Webhook delivery
• API export
```

### TUI Advanced Features

#### Multi-pane Layouts
```bash
# Split view: Projects | Results
openclaw tui --layout split

# Tab view: Multiple tabs
openclaw tui --layout tabs

# Full screen: Single pane
openclaw tui --layout full
```

#### Advanced Filtering
```
TUI Filter Syntax:

By severity:
  filter severity >= HIGH

By type:
  filter type = security

By date:
  filter created >= 2024-05-01

Combined:
  filter severity = HIGH && type = performance
```

#### Save & Load Sessions
```bash
# Save current session
:save-session my-session

# Load session
:load-session my-session

# List sessions
:sessions

# Session auto-save
opencloud tui --auto-save
```

### Development Workflow
```
Code → Scan → Review → Test → Deploy
  ↓      ↓       ↓      ↓      ↓
  Write  Find    Fix    Gen    Push
  Code   Issues  Issues Tests  Update
```

### Quality Assurance Workflow
```bash
# Pre-commit
openclaw pre-commit

# Pre-push
openclaw pre-push --check-tests
openclaw security-scan

# CI/CD Integration
openclaw ci --report
```

### Code Review Workflow
```bash
# Analyze PR
openclaw review --pr-number 123

# Generate suggestions
openclaw suggestions --context pull-request

# Export review
openclaw review export --format markdown > review.md
```

### Team Onboarding
```bash
# Generate project overview
openclaw docs generate --audience=new-team-member

# Create architecture guide
openclaw architecture document

# Setup IDE configurations
openclaw ide setup --preset team-standard
```

### Best Practices
1. **Regular scanning** - daily/on-commit
2. **Model selection** - match to task complexity
3. **Caching** - enable for repeated analyses
4. **Review first** - don't auto-apply suggestions
5. **Team standards** - establish baselines
6. **Automation** - CI/CD integration essential
7. **Monitoring** - track metrics over time

## Skills & Tools

### Built-in Skills

#### Language Skills
- **JavaScript/TypeScript**: React, Vue, Angular, Node.js
- **Python**: Django, Flask, FastAPI, Data Science
- **Java**: Spring Boot, Spring Cloud, Microservices
- **Go**: Concurrency patterns, performance
- **Rust**: Memory safety, systems programming

#### Domain Skills
- **Security**: OWASP, CWE detection
- **Performance**: Profiling, optimization
- **Testing**: Coverage, mutation testing
- **Documentation**: API docs, README generation
- **Architecture**: Design patterns, microservices

### Installing Skills
```bash
# List available
openclaw skills list

# Install skill
openclaw skills install security-analyzer

# Activate for project
openclaw project skill activate security-analyzer
```

### Custom Tools
```bash
# Create custom tool
openclaw tools create --name my-analyzer

# Define tool behavior
openclaw tools config my-analyzer --config ./config.yaml

# Use in analysis
openclaw analyze --tool my-analyzer ./src
```

### Tool Chaining
```yaml
# tools/workflow.yaml
name: security-and-performance
description: Combined security and performance analysis
tools:
  - security-analyzer
  - performance-profiler
  - test-coverage
flow: sequential
```

### Extending with Custom Rules
```python
# .openclaw/rules/custom.py
from openclaw import Rule, Severity

class CustomSecurityRule(Rule):
    name = "custom_security_check"
    severity = Severity.HIGH
    
    def check(self, code):
        # Your analysis logic
        return issues
```

## Advanced Usage

### Batch Processing
```bash
# Process multiple projects
openclaw batch --config batch.yaml

# Process directories
openclaw scan --recursive ./projects/
```

### Custom Configurations
```yaml
# .openclaw/advanced.yml
analysis:
  depth: deep
  parallel: true
  workers: 4
  cache:
    enabled: true
    ttl: 86400
  
reporting:
  formats: [json, html, markdown]
  export_path: ./reports/
```

### Scripting and Automation
```bash
#!/bin/bash
# Analyze all branches
for branch in $(git branch -r); do
  git checkout $branch
  openclaw scan --output ./reports/${branch}.json
done
```

### Performance Optimization
```bash
# Enable caching
openclaw cache enable

# Use parallel processing
openclaw analyze --parallel --workers 8

# Stream large files
openclaw analyze --stream ./large-file.py
```

## Troubleshooting

### Connection Issues
```bash
# Test API connectivity
openclaw health-check

# Verify credentials
openclaw auth verify

# Reconnect
openclaw auth refresh
```

### Analysis Issues
```bash
# Clear cache
openclaw cache clear

# Enable debug logging
openclaw --debug analyze ./src

# Check logs
openclaw logs tail -f 100
```

### Performance Issues
```bash
# Reduce workers
openclaw config set workers 2

# Enable streaming
openclaw analyze --stream ./src

# Use faster model
openclaw analyze --model claude-3-haiku ./src
```

### Database Issues
```bash
# Reset database
openclaw db reset

# Migrate database
openclaw db migrate

# Check database status
openclaw db status
```

### Getting Help
- Docs: https://openclaw.docs/
- Issues: https://github.com/openclaw/openclaw/issues
- Community: https://openclaw.community/
- Support: support@openclaw.io
- Discord: https://discord.gg/openclaw

## Complementary Tools & Free Integrations

### Code Quality & Analysis (Free)

#### SonarQube Community Edition
- Free self-hosted
- Integrates with OpenClaw findings
- Deep code metrics

#### Codeclimate / CodeFactor
- Some free tiers available
- Complements OpenClaw

### Testing & Coverage (Free & Open Source)

```bash
npm install -D jest              # JavaScript
pip install pytest               # Python
npm install nyc                  # Coverage reports
```

### Security Tools (Free & Open Source)

#### OWASP ZAP
- Free security scanner
- Works with OpenClaw findings

#### Snyk (Free Tier)
- Dependency scanning
- 1 free project

#### Git-secrets
```bash
git secrets install             # Detect secrets
```

### CI/CD Automation (Free)

#### GitHub Actions
```yaml
name: OpenClaw Analysis
on: [pull_request]
jobs:
  scan:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - run: openclaw scan
```

#### GitLab CI / Jenkins
- Free tiers
- Easy OpenClaw integration

### Database Tools (Free)

#### PostgreSQL / MongoDB
- 100% free & open source
- Free cloud tiers (Supabase, Atlas)

#### DBeaver / MongoDB Compass
- Free SQL IDE
- Visual tools

### Hosting & Deployment (Free Tiers)

- **Vercel**: Free tier
- **Railway**: $5 credit/month
- **Render**: Free tier
- **Heroku**: Free eco dynos

### Container Tools (Free)

- **Docker**: Community free
- **Podman**: Open source alternative
- **Kubernetes**: minikube, kind, k3s (all free)

### Monitoring (Free Tiers)

#### New Relic
- Free forever tier
- APM & monitoring

#### Prometheus + Grafana
- 100% open source
- Self-hosted monitoring

### Collaboration (Free)

- **GitHub**: Free tier (very generous)
- **GitLab**: Free tier
- **Discord**: Free team communication

## Free Tech Stack Example

```
Analysis:     OpenClaw
Testing:      Jest/Pytest (Free)
CI/CD:        GitHub Actions (Free)
Hosting:      Railway/Vercel (Free tier)
Database:     PostgreSQL (Free)
Monitoring:   New Relic (Free forever)
Containers:   Docker (Free)
Total:        ~$0-20/month
```

## Free Learning Resources

- **MDN Web Docs**: https://developer.mozilla.org
- **freeCodeCamp**: https://freecodecamp.org  
- **Dev.to**: https://dev.to
- **Stack Overflow**: https://stackoverflow.com
- **Coursera**: Audit courses free
