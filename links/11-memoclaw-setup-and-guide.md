# MemoClaw - Complete Setup & User Guide

## Table of Contents
1. [Installation & Setup](#installation--setup)
2. [Getting Started](#getting-started)
3. [Model Configuration](#model-configuration)
4. [Core Features](#core-features)
5. [Memory Management](#memory-management)
6. [Workflows & Best Practices](#workflows--best-practices)
7. [Skills & Capabilities](#skills--capabilities)
8. [Optimization](#optimization)
9. [Troubleshooting](#troubleshooting)

## Installation & Setup

### Prerequisites
- Python 3.10+
- Redis 6.0+ (for caching layer)
- 4GB+ RAM (recommended)
- Modern CPU (multi-core preferred)
- Network connectivity

### Installation

#### Docker Installation (Recommended)
```bash
# Docker Compose setup
git clone https://github.com/nemoclaw/memoclaw.git
cd memoclaw

# Build and run
docker-compose up -d

# Verify installation
docker-compose exec memoclaw memoclaw --version
```

#### Local Installation
```bash
# Install package
pip install memoclaw

# Initialize environment
memoclaw init

# Configure settings
memoclaw config setup

# Start service
memoclaw service start
```

### Configuration
```bash
# Set core parameters
memoclaw config set cache-backend redis
memoclaw config set cache-size 2GB
memoclaw config set ttl 3600

# Set model
memoclaw config set model claude-3-5-sonnet

# Enable features
memoclaw config enable memory-persistence
memoclaw config enable distributed-cache
```

## User Interface & Dashboard

### Web Dashboard Access
Web UI available at `http://localhost:8080`

#### Dashboard Features
- **Memory Status**: Visual representation of memory usage
- **Knowledge Graph**: Graphical view of stored relationships
- **Analysis History**: Timeline of learning and analysis
- **Pattern Recognition**: Identified code patterns visualization
- **Team Memory**: Shared knowledge across team
- **Memory health**: Fragmentation, performance metrics

#### Web Dashboard Panels
```
┌──────────────────────────────────────────────────┐
│ MemoClaw - Memory Dashboard                      │
├──────────────────────────────────────────────────┤
│ Home │ Memory Graph │ History │ Patterns │ Team  │
├──────────────────────────────────────────────────┤
│ ┌────────────────┐  ┌───────────────────────┐   │
│ │ Memory Usage   │  │ Recent Learning       │   │
│ │ 2.3GB / 4GB    │  │ • API Patterns: +5    │   │
│ │ ████░░░░░░░░░ │  │ • Bug Fixes: +2       │   │
│ └────────────────┘  │ • Optimizations: +8   │   │
│                     └───────────────────────┘   │
│ ┌────────────────┐  ┌───────────────────────┐   │
│ │ Knowledge Base │  │ Team Contributions    │   │
│ │ 847 patterns   │  │ • Alice: +125 entries │   │
│ │ 512 learnings  │  │ • Bob: +89 entries    │   │
│ └────────────────┘  └───────────────────────┘   │
└──────────────────────────────────────────────────┘
```

#### Web Workflows
```
View Memory Graph:
1. Dashboard → Memory Graph
2. See all connected patterns
3. Click nodes to expand
4. Search for relationships
5. Export visualization

Query Memory:
1. Dashboard → Memory Query
2. Type question
3. See relevant patterns
4. Click to see details
5. Add feedback/corrections
```

### Terminal UI (TUI)
Start interactive memory interface:
```bash
memoclaw tui
```

#### TUI Commands
```
Memory Commands:
  memory list         → Show all stored patterns
  memory search <term> → Search knowledge base
  memory query <q>    → Ask memory questions
  memory stats        → Show memory usage
  memory graph        → Display knowledge graph
  memory export       → Export all knowledge
  
Pattern Management:
  patterns list       → List learned patterns
  patterns view <id>  → Show pattern details
  patterns tag <name> → Tag pattern
  patterns relate <id> → Find relationships
  patterns remove <id> → Delete pattern
  
Analysis:
  analyze <file>      → Analyze with memory
  analyze --deep      → Deep analysis (Opus)
  analyze --fast      → Quick analysis (Haiku)
  
Learning:
  learn-patterns      → Discover new patterns
  learn-update        → Update learning
  learn-feedback      → Provide correction
  learn-export        → Export learnings
  
Settings:
  memory-level set    → Set memory tier
  cache-ttl set       → Configure expiry
  pruning enable/off  → Auto-pruning
```

#### TUI Keyboard Shortcuts
```
Navigation:
  ↑/↓         → Move through patterns
  /           → Search patterns
  Tab         → Switch panes
  g           → Go to top
  G           → Go to bottom
  
Memory Operations:
  v           → View details
  e           → Edit pattern
  t           → Add tag
  r           → Show relations
  d           → Delete
  c           → Copy
  j           → Next related
  k           → Prev related
```

#### TUI Memory Visualization
```bash
# Show memory graph
memoclaw tui --view graph

# Show hierarchical tree
memoclaw tui --view tree

# Show table view
memoclaw tui --view table

# Interactive exploration
memoclaw tui --interactive
```

### Memory Query Interface

#### Query Syntax
```bash
# Find patterns
memoclaw memory query "react hooks patterns"

# Find similar code
memoclaw memory query-similar ./myfile.js

# Get recommendations
memoclaw memory recommend "api design"

# Historical analysis
memoclaw memory timeline --pattern-type "optimization"
```

#### Query Results Display
```
Query: "error handling patterns"

Results:
├─ Try-Catch Pattern (45 occurrences)
│  ├─ Usage: Exception handling
│  ├─ Language: JavaScript/Python
│  └─ Files: error-handler.js, utils.py
│
├─ Custom Error Classes (28 occurrences)
│  ├─ Usage: Domain errors
│  └─ Example: class ValidationError
│
└─ Middleware Error Pattern (12 occurrences)
   └─ Usage: Express error handling
```

## Getting Started

### First Steps
```bash
# Initialize project
memoclaw project init --name myproject

# Create memory profile
memoclaw memory create-profile

# Run first analysis
memoclaw analyze --enable-memory ./src
```

### Basic Commands
```bash
# Process with memory
memoclaw process --memory-enabled ./code

# Query memory
memoclaw memory query "what's the architecture?"

# List stored knowledge
memoclaw memory list

# Export knowledge
memoclaw memory export --format json
```

### Understanding Memory
- **Short-term**: Current session context
- **Long-term**: Persistent knowledge base
- **Working**: Active problem context
- **Reference**: Code patterns and standards

## Model Configuration

### Model Selection
```bash
# Default model
claude-3-5-sonnet

# For memory-intensive tasks
claude-3-opus

# For lightweight operations
claude-3-haiku
```

### Model with Memory
```yaml
# memoclaw.yml
model:
  primary: claude-3-5-sonnet
  fallback: claude-3-haiku
  memory_aware: true
  context_window: 8000
  memory_allocation: 4000  # tokens for memory
```

### Context Management
```bash
# Set context size
memoclaw config set context-window 12000

# Reserve memory for retrieval
memoclaw config set memory-reserve 3000

# Enable smart pruning
memoclaw config set pruning smart
```

## Core Features

### Memory Capabilities
- **Persistent Memory**: Long-term knowledge retention
- **Contextual Recall**: Smart retrieval relevant to current task
- **Pattern Recognition**: Identify recurring issues
- **Knowledge Graph**: Relationships between concepts
- **Semantic Search**: Find related information

### Analysis Features
- **Code Understanding**: Deep semantic analysis
- **Pattern Detection**: Architectural and code patterns
- **Dependency Mapping**: Relationship tracking
- **Risk Assessment**: Potential issues
- **Optimization Suggestions**: Performance improvements

### Generation Features
- **Context-Aware Code**: Generated with memory context
- **Documentation**: Auto-generated with pattern knowledge
- **Test Cases**: Based on code patterns
- **Refactoring**: Using architectural knowledge
- **Implementation Guides**: Drawing from similar patterns

### Memory Operations
```bash
# Store code pattern
memoclaw memory store-pattern "react-hooks" ./patterns/

# Tag memory entry
memoclaw memory tag "api-design" patterns/rest-api

# Search memory
memoclaw memory search "similar patterns" --context api

# Update memory
memoclaw memory update "react-hooks" ./new-patterns/

# Prune old entries
memoclaw memory prune --older-than 30days
```

## Memory Management

### Memory Hierarchy
```
Level 1: Session Memory (Current work)
   ↓
Level 2: Project Memory (Project context)
   ↓
Level 3: Team Memory (Shared knowledge)
   ↓
Level 4: Global Memory (General patterns)
```

### Configuring Storage
```yaml
# memoclaw-storage.yml
storage:
  backend: redis
  persistence: postgresql
  cache_ttl: 86400
  
memory_levels:
  session:
    max_size: 100MB
    decay: fast
  project:
    max_size: 500MB
    decay: medium
  team:
    max_size: 2GB
    decay: slow
  global:
    max_size: unlimited
    decay: never
```

### Memory Persistence
```bash
# Save session memory
memoclaw memory checkpoint

# Load previous memory
memoclaw memory load session-2024-05-08

# Export for sharing
memoclaw memory package --output knowledge.tar.gz

# Import team knowledge
memoclaw memory import knowledge.tar.gz
```

### Memory Optimization
```bash
# Analyze memory usage
memoclaw memory stats

# Optimize storage
memoclaw memory optimize

# Archive old memory
memoclaw memory archive --older-than 90days

# Clean unused
memoclaw memory cleanup
```

## Workflows & Best Practices

### Development Workflow with Memory
```
Start Project → Initialize Memory
    ↓
Write Code → Build Memory Context
    ↓
Analyze → Use Accumulated Knowledge
    ↓
Generate Tests → Reference Similar Patterns
    ↓
Deploy → Store Deployment Knowledge
```

### Memory-Aware Code Review
```bash
# Analyze PR with memory
memoclaw review --with-memory PR-123

# Check against known patterns
memoclaw review --memory-baseline

# Generate contextual suggestions
memoclaw review --memory-context
```

### Team Knowledge Building
```bash
# Initialize team memory
memoclaw team memory init

# Share patterns
memoclaw memory share pattern-name --team

# Aggregate learnings
memoclaw memory aggregate --team
```

### Best Practices
1. **Regular memory checkpoints** - save progress
2. **Tag important concepts** - for retrieval
3. **Share patterns** - team learning
4. **Archive old knowledge** - storage optimization
5. **Review memory** - keep it accurate
6. **Use semantic search** - find relevant context
7. **Monitor memory health** - prevent bloat

## Skills & Capabilities

### Memory Skills
- **Pattern Recognition**: Identify recurring code patterns
- **Architectural Understanding**: System design analysis
- **Performance Patterns**: Optimization knowledge
- **Security Patterns**: Vulnerability patterns
- **API Design**: REST, GraphQL patterns

### Language-Specific Skills
- **JavaScript/TypeScript**: Framework patterns, async patterns
- **Python**: Data handling, async patterns
- **Java**: Spring patterns, microservices
- **Go**: Concurrency patterns
- **Rust**: Memory safety patterns

### Activating Skills
```bash
# Enable pattern recognition
memoclaw skills enable pattern-recognition

# Activate language skills
memoclaw skills enable javascript-patterns
memoclaw skills enable python-data-patterns

# Custom skills
memoclaw skills create custom-skill --template pattern
```

### Building Custom Memory Skills
```python
# .memoclaw/skills/custom_skill.py
from memoclaw import MemorySkill

class CustomPatternSkill(MemorySkill):
    name = "custom_patterns"
    
    def learn_pattern(self, code):
        """Extract pattern from code"""
        return pattern
    
    def apply_pattern(self, context):
        """Apply stored patterns"""
        return suggested_code
```

## Optimization

### Performance Tuning
```bash
# Enable fast mode
memoclaw config set mode fast

# Increase cache
memoclaw config set cache-size 4GB

# Enable distributed cache
memoclaw config enable distributed-cache

# Parallel processing
memoclaw process --parallel --workers 8
```

### Memory Efficiency
```bash
# Analyze memory profile
memoclaw memory profile

# Enable compression
memoclaw config set compression zstd

# Use sparse indexing
memoclaw config set indexing sparse

# Set memory limits
memoclaw config set max-memory 3GB
```

### Caching Strategy
```yaml
# memoclaw-cache.yml
cache:
  redis:
    host: localhost
    port: 6379
    db: 0
  compression: true
  ttl:
    short_term: 300
    medium_term: 3600
    long_term: 86400
```

## Troubleshooting

### Memory Issues
```bash
# Check memory status
memoclaw memory status

# Diagnose issues
memoclaw memory diagnose

# Rebuild indexes
memoclaw memory rebuild-indexes

# Clear corrupted data
memoclaw memory repair
```

### Performance Issues
```bash
# Profile performance
memoclaw profile --detailed

# Identify bottlenecks
memoclaw memory analyze-bottlenecks

# Reduce memory size
memoclaw memory prune --aggressive

# Switch to lite mode
memoclaw config set mode lite
```

### Connection Issues
```bash
# Check Redis connection
memoclaw redis ping

# Test database connection
memoclaw db test

# Reset connections
memoclaw connections reset
```

### Recovery
```bash
# Restore from checkpoint
memoclaw memory restore --checkpoint latest

# Import backup
memoclaw memory restore --backup backup-file.tar.gz

# Reset and reinitialize
memoclaw memory reset --confirm
```

### Getting Help
- Documentation: https://memoclaw.docs/
- Examples: https://memoclaw.docs/examples
- Issues: https://github.com/nemoclaw/memoclaw/issues
- Community: https://memoclaw.community/
- Support: support@memoclaw.io

## Complementary Tools & Free Integrations

### Graph Databases (Store Knowledge)

#### Neo4j Community Edition
- Free graph database
- Perfect for knowledge graphs
- Visualizes relationships

#### ArangoDB
- Free multi-model database
- Document + graph support

### Knowledge Management (Free)

#### WikiJS
- Free modern wiki
- Knowledge sharing
- Self-hosted

#### Obsidian
- Free personal knowledge base
- Works with MemoClaw exports

### Code Analysis & Patterns (Free)

#### Semgrep
- Free pattern detection
- Code search capabilities

#### AST-grep
- Free code searching
- Pattern matching

### Memory & Caching (Free & Open Source)

#### Redis
- Free in-memory cache
- Perfect for MemoClaw
- Open source

#### Valkey
- Redis fork
- 100% free

### Testing (Free & Open Source)

- **Jest**: JavaScript testing
- **Pytest**: Python testing
- Generate tests from MemoClaw patterns

### CI/CD (Free)

#### GitHub Actions
```yaml
name: MemoClaw Learning
on: [push]
jobs:
  learn:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - run: memoclaw learn-patterns ./src
```

### Visualization Tools (Free)

#### Mermaid
- Diagram as code
- Visualize knowledge graphs

#### Graphviz
- Graph visualization
- Free & open source

#### D3.js
- Interactive visualizations

### Machine Learning (Free)

#### Sentence-Transformers
- Free embeddings
- Semantic search

#### FastText
- Word embeddings free
- Facebook open source

### Storage & Backup (Free)

#### PostgreSQL
- Persistent storage
- Free & open source

#### Restic
- Free encrypted backups
- Incremental backups

### Monitoring (Free Tiers)

#### Prometheus + Grafana
- 100% open source
- Self-hosted monitoring

#### New Relic / Datadog
- Free forever tiers

## Free Tech Stack for MemoClaw

```
Memory Cache:     Redis (Free)
Persistent DB:    PostgreSQL (Free)
Graph DB:         Neo4j Community (Free)
Wiki:             WikiJS (Free)
CI/CD:            GitHub Actions (Free)
Monitoring:       Prometheus (Free)
Visualization:    Mermaid (Free)
Total:            ~$0-15/month
```

## Free Learning Resources

- **Redis Docs**: https://redis.io/docs
- **PostgreSQL Docs**: https://postgresql.org/docs
- **freeCodeCamp**: https://freecodecamp.org
- **Dev.to**: https://dev.to
- **Stack Overflow**: https://stackoverflow.com
