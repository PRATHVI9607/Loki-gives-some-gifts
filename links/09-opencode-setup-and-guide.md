# OpenCode - Complete Setup & User Guide

## Table of Contents
1. [Installation & Setup](#installation--setup)
2. [Getting Started](#getting-started)
3. [Model Configuration](#model-configuration)
4. [Features & Capabilities](#features--capabilities)
5. [Workflows & Best Practices](#workflows--best-practices)
6. [Skills & Extensions](#skills--extensions)
7. [Troubleshooting](#troubleshooting)

## Installation & Setup

### Prerequisites
- Python 3.8 or higher
- Node.js 14+ (for certain integrations)
- Git
- 4GB RAM minimum
- Code editor or IDE

### Installation Steps

```bash
# Clone the repository
git clone https://github.com/opencode/opencode.git
cd opencode

# Install dependencies
pip install -r requirements.txt

# Configure environment
cp .env.example .env
# Edit .env with your settings
```

### Configuration
Create your `.env` file:
```
OPENCODE_API_KEY=your_key_here
OPENCODE_MODEL=claude-3-5-sonnet
OPENCODE_DEBUG=false
OPENCODE_PORT=8000
```

## User Interface & Dashboard

### Web Dashboard
Access the interactive web UI at `http://localhost:8080`

#### Dashboard Features
- **Project Overview**: Visual project structure and metrics
- **Analysis Results**: Interactive charts and detailed reports
- **Code Diff Viewer**: Syntax-highlighted code comparisons
- **Recommendations**: Actionable insights with explanations
- **Team Collaboration**: Shared workspaces and comments
- **Real-time Updates**: Live analysis progress

#### Dashboard Sections
```
Home → Projects → Select Project → Analysis Dashboard
       ↓
  • Code Quality Score (0-100)
  • Issues by Severity (High/Medium/Low)
  • Test Coverage %
  • Performance Metrics
  • Recent Changes
  • Team Activity
```

#### Key Dashboard Operations
1. **View Analysis**: Click project → see live results
2. **Filter Issues**: By type, severity, file
3. **Add Comments**: Collaborate on specific findings
4. **Export Reports**: PDF, JSON, CSV formats
5. **Share Analysis**: Generate shareable links
6. **Configure Alerts**: Set thresholds for notifications

### Terminal UI (TUI)
Run interactive TUI mode:
```bash
opencode tui
```

#### TUI Navigation
```
┌─────────────────────────────┐
│ OpenCode TUI v1.0           │
├─────────────────────────────┤
│ [P]rojects  [A]nalyze       │
│ [R]eports   [S]ettings      │
│ [H]elp      [Q]uit          │
└─────────────────────────────┘
```

#### TUI Commands
```
Project Management:
  P           → Project list
  N           → New project
  O           → Open project
  D           → Delete project

Analysis:
  A           → Start analysis
  C           → Cancel analysis
  R           → View results
  E           → Export report

Navigation:
  ↑/↓         → Move up/down
  Enter       → Select
  ESC         → Go back
  Ctrl+C      → Exit

Filtering:
  /           → Search
  F           → Filter by type
  S           → Sort options
```

#### TUI Features
- **Real-time Progress**: Watch analysis live
- **Interactive Results**: Filter and drill-down
- **Quick Actions**: Keyboard shortcuts
- **Color Coding**: Issues by severity (Red/Yellow/Green)
- **Performance**: Optimized for large datasets

### VS Code Extension UI (if available)
```
Sidebar Integration:
├── OpenCode Logo
│   ├── Projects
│   ├── Recent Analysis
│   ├── Settings
│   └── Help
```

## Getting Started

### Basic Usage
```bash
# Start OpenCode server (enables all UIs)
opencode start

# Initialize a new project
opencode init --name my-project

# Run analysis
opencode analyze ./src

# Launch TUI
opencode tui

# Open Web Dashboard
opencode open --web   # Opens http://localhost:8080
```

### First Project - Via Web UI
```
1. Visit http://localhost:8080
2. Click "New Project" button
3. Fill in project details:
   - Name, Language, Framework
4. Configure integrations (Optional)
5. Click "Create"
6. Dashboard opens with empty analysis
```

### First Project - Via TUI
```bash
opencode tui
# Press 'N' for New Project
# Follow menu prompts
# Project created and appears in list
```

### First Project - Via CLI
```bash
# Create project structure
opencode create-project
# Follow interactive prompts
# Select your tech stack
# Configure integrations
```

## Advanced UI Features

### Web Dashboard Advanced Features

#### Custom Dashboards
- Create personalized dashboard layouts
- Drag-and-drop widgets
- Save custom views for team
- Share dashboard templates

#### Team Collaboration
```
Right-click issue in Dashboard:
  • Add comment
  • Mention team members (@name)
  • Assign to developer
  • Link to issue tracker
  • Mark as resolved
  • Schedule discussion
```

#### Real-time Notifications
```
Dashboard → Settings → Notifications
  ✓ Critical issues found
  ✓ Analysis completed
  ✓ Team comments
  ✓ Coverage drops
  ✓ Performance regressions
```

#### Report Generation
```
Dashboard → Reports → Generate
  • Executive Summary
  • Technical Details
  • Metrics Trends
  • Recommendations
  • Team Velocity
  • Quality Evolution
```

### TUI Advanced Features

#### Keyboard Shortcuts
```
Analysis Navigation:
  Tab         → Switch between panes
  Shift+Tab   → Previous pane
  j/k         → Down/Up (vim style)
  g g         → Go to top
  G           → Go to bottom
  :number     → Jump to line

Results Manipulation:
  Ctrl+F      → Find in results
  Ctrl+A      → Select all
  Ctrl+C      → Copy
  Ctrl+X      → Cut

Actions:
  Space       → Toggle selection
  Enter       → Open/Execute
  D           → Delete/Dismiss
  E           → Edit/Explain
  X           → Execute fix
```

#### TUI Themes
```bash
opencode tui --theme dark      # Dark theme
opencode tui --theme light     # Light theme
opencode tui --theme monokai   # Monokai
opencode tui --theme solarized # Solarized
```

#### Custom TUI Layouts
```bash
# Save current layout
opencode tui --save-layout my-layout

# Load saved layout
opencode tui --load-layout my-layout

# List saved layouts
opencode tui --list-layouts
```

## Model Configuration

### Available Models
- **claude-3-5-sonnet**: Recommended for most use cases
- **claude-3-opus**: Best for complex reasoning
- **claude-3-haiku**: Fast, lightweight tasks

### Switching Models
```bash
# Set default model
opencode config set model claude-3-opus

# Use specific model for task
opencode analyze --model claude-3-haiku ./src
```

### Model Parameters
```yaml
# In opencode.yaml
models:
  default: claude-3-5-sonnet
  options:
    temperature: 0.7
    max_tokens: 4096
    top_p: 0.9
```

### Performance Optimization
- **Haiku** for rapid iteration
- **Sonnet** for balanced quality/speed
- **Opus** for deep analysis
- Use caching to reduce API calls

### Switch Model via Web UI
```
1. Go to Dashboard → Settings → Model
2. Select model from dropdown
3. View estimated performance impact
4. Click "Apply"
5. Restart analysis if needed
```

### Switch Model via TUI
```
Press 'S' for Settings
Navigate to Model
Select with arrow keys and Enter
Changes apply immediately
```

## Features & Capabilities

### Code Analysis
- Static code analysis
- Security vulnerability detection
- Performance profiling
- Code quality metrics
- Dependency analysis

### Code Generation
- Function generation from descriptions
- Test case generation
- Documentation generation
- Boilerplate scaffolding
- Refactoring suggestions

### Integration Capabilities
- Git integration
- CI/CD pipeline integration
- IDE plugins
- Slack notifications
- Webhook support

### Advanced Features
- Custom rulesets
- Multi-language support
- Batch processing
- Real-time collaboration
- Version control integration

## Workflows & Best Practices

### Daily Development Workflow
```
1. Start project → opencode init
2. Write code → opencode lint (as you go)
3. Generate tests → opencode test-gen
4. Document → opencode doc-gen
5. Deploy → opencode deploy
```

### Code Review Workflow
```bash
# Analyze pull request
opencode review --pr-url https://github.com/...

# Generate review report
opencode report --format markdown > review.md
```

### Onboarding Workflow
```bash
# Generate documentation for new team members
opencode onboard --generate-docs

# Create architecture overview
opencode architecture --output docs/architecture.md
```

### Best Practices
- Run analysis before commits
- Use appropriate model sizes for tasks
- Enable caching for repeated analysis
- Set up CI/CD integration
- Review generated code before merging
- Keep models updated

## Skills & Extensions

### Built-in Skills
- **JavaScript/TypeScript**: Full support for web frameworks
- **Python**: Django, Flask, FastAPI optimization
- **Java**: Spring Boot, Maven integration
- **Go**: Microservices patterns
- **Rust**: Systems programming best practices

### Creating Custom Skills
```yaml
# skills/my-skill.yaml
name: my-skill
version: 1.0.0
description: Custom analysis skill
triggers:
  - pattern: "*.custom"
  - command: "my-skill"
actions:
  - analyze
  - suggest
  - generate
```

### Popular Extensions
- **opencode-prettier**: Code formatting
- **opencode-eslint**: Linting integration
- **opencode-coverage**: Coverage tracking
- **opencode-performance**: Performance monitoring

### Installing Extensions
```bash
opencode install-extension opencode-prettier
opencode extension list
opencode extension update
```

### Building Custom Extensions
```typescript
// extensions/my-extension/index.ts
export default {
  name: 'my-extension',
  version: '1.0.0',
  register(api) {
    api.registerAnalyzer('custom', analyzerFunction);
  }
}
```

## Troubleshooting

### Common Issues

**Issue: API key not recognized**
```bash
# Verify key in environment
echo $OPENCODE_API_KEY
# Regenerate key if needed
opencode auth regenerate
```

**Issue: Slow analysis**
```bash
# Clear cache
opencode cache clear

# Use faster model
opencode config set model claude-3-haiku

# Enable parallel processing
opencode analyze --parallel ./src
```

**Issue: Memory errors**
```bash
# Reduce batch size
opencode config set batch_size 10

# Enable streaming mode
opencode analyze --stream ./src
```

### Getting Help
- Documentation: https://opencode.docs/
- Issues: https://github.com/opencode/opencode/issues
- Community: https://opencode.community/
- Support: support@opencode.io

## Complementary Tools & Free Integrations

### Code Quality Tools (Free & Open Source)

#### ESLint (JavaScript/TypeScript)
```bash
npm install -D eslint prettier
# OpenCode uses ESLint rules for suggestions
```

#### Pylint (Python)
```bash
pip install pylint black
# Python code quality tools
```

#### SonarQube Community Edition
- Free self-hosted version
- Integrates with OpenCode
- Deep code metrics & dashboards

### Testing Frameworks (All Free)
- **Jest**: JavaScript testing
- **Pytest**: Python testing  
- **JUnit**: Java testing
- OpenCode generates tests for all

### CI/CD Integration (Free)

#### GitHub Actions
```yaml
name: OpenCode Analysis
on: [push]
jobs:
  analyze:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - run: opencode analyze ./src
```

#### GitLab CI / Jenkins
- Free tiers available
- Direct OpenCode integration

### Monitoring & Analytics (Free Tiers)

#### New Relic
- Free forever tier
- Works with OpenCode metrics

#### Sentry
- Free: 10k errors/month
- Error tracking

### Database & Storage (Free & Open Source)

#### PostgreSQL / MongoDB
- 100% free & open source
- Free cloud tiers available

#### Redis
- Free in-memory caching
- Open source

### Hosting (Free Tiers)

- **Vercel**: Free tier
- **Netlify**: Free tier
- **Railway**: $5 credit/month
- **Render**: Free tier

### Container Tools (Free)

- **Docker**: Community edition free
- **Podman**: Docker alternative (100% free)

## Free Learning Resources

- **MDN Web Docs**: https://developer.mozilla.org
- **freeCodeCamp**: https://freecodecamp.org
- **Dev.to**: https://dev.to (free articles)
- **Stack Overflow**: https://stackoverflow.com
- **Reddit**: r/programming, r/devops
