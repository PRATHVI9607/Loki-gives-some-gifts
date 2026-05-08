# NVIDIA Kimic 2.6 & Free Model Setup with OpenCode

## Table of Contents
1. [What is NVIDIA Kimic 2.6](#what-is-nvidia-kimic-26)
2. [Installation & Setup](#installation--setup)
3. [Integration with OpenCode](#integration-with-opencode)
4. [Configuration Guide](#configuration-guide)
5. [Usage & Features](#usage--features)
6. [API Integration](#api-integration)
7. [Performance Optimization](#performance-optimization)
8. [Troubleshooting](#troubleshooting)

## What is NVIDIA Kimic 2.6

### Overview
NVIDIA Kimic 2.6 is a free large language model provided by NVIDIA for developers and researchers:

- **Free Forever**: No cost, no credit card required
- **Open Weights**: Can be self-hosted or used via API
- **Purpose**: Code generation, analysis, and optimization
- **Performance**: Excellent for code-related tasks
- **LocalBoost**: Run locally or use cloud API

### Key Advantages
```
✓ Complete free - no hidden costs
✓ Self-hosted option available
✓ Works offline (local deployment)
✓ Perfect complement to OpenCode
✓ No rate limiting on local deployment
✓ Open source weights
✓ Community support
```

### Supported Use Cases
- Code analysis and review
- Automated bug detection
- Performance optimization suggestions
- Documentation generation
- Test case creation
- Code refactoring

## Installation & Setup

### Prerequisites
- Python 3.10+
- CUDA 11.8+ (for GPU acceleration - optional but recommended)
- 8GB+ RAM (16GB recommended)
- GPU: NVIDIA GPU with 4GB+ VRAM (or CPU-only mode)
- pip package manager
- Git

### Option 1: Cloud API Setup (Easiest)

#### Get API Key from NVIDIA
```bash
# Visit NVIDIA's free model portal
# https://nvidia.com/ai/kimic

# Sign up for free account
# Generate API key in dashboard
# Copy API key to clipboard
```

#### Configure Environment
```bash
# Create .env file
cat > .env << EOF
NVIDIA_API_KEY=your_api_key_here
NVIDIA_MODEL=nvidia/kimic-2.6
NVIDIA_BASE_URL=https://api.nvidia.com/v1/endpoints
EOF

# Source environment
source .env          # macOS/Linux
$env:NVIDIA_API_KEY="your_key"  # Windows PowerShell
```

### Option 2: Local Docker Deployment (Recommended)

#### Pull NVIDIA Container
```bash
docker pull nvcr.io/nvidia/kimic:2.6-latest

# Run container
docker run -d \
  --name kimic \
  --gpus all \
  -p 8000:8000 \
  -e NVIDIA_VISIBLE_DEVICES=all \
  nvcr.io/nvidia/kimic:2.6-latest
```

#### Verify Running
```bash
curl http://localhost:8000/health
# Response: {"status": "healthy"}
```

### Option 3: Local Python Setup

#### Install from NVIDIA
```bash
# Install NVIDIA package
pip install nvidia-kimic

# Or from source
git clone https://github.com/NVIDIA/Kimic.git
cd Kimic
pip install -e .
```

#### Initialize Model
```bash
kimic download --model kimic-2.6-full
# Downloads ~30GB model weights

# Or lightweight version
kimic download --model kimic-2.6-lite
# Downloads ~8GB (CPU-friendly)
```

#### Start Local Server
```bash
# Start API server on localhost:8000
kimic serve --model kimic-2.6 --port 8000

# With GPU acceleration
kimic serve --model kimic-2.6 --device cuda:0 --port 8000

# CPU only mode
kimic serve --model kimic-2.6-lite --device cpu --port 8000
```

### Option 4: Hugging Face Integration

#### Download from Hugging Face
```bash
# Install transformers
pip install transformers torch

# Download model
python -c "
from transformers import AutoModelForCausalLM, AutoTokenizer
model = AutoModelForCausalLM.from_pretrained('nvidia/kimic-2.6')
tokenizer = AutoTokenizer.from_pretrained('nvidia/kimic-2.6')
"

# Then use locally
python scripts/inference.py
```

## Integration with OpenCode

### Connect OpenCode to Kimic 2.6

#### Configuration File
Create `opencode.yml`:
```yaml
model:
  provider: nvidia
  model_name: kimic-2.6
  api_type: local          # or "cloud"
  base_url: http://localhost:8000
  api_key: ${NVIDIA_API_KEY}
  
settings:
  # Code analysis
  analyze_depth: deep
  generate_tests: true
  security_scan: true
  
  # Performance
  max_tokens: 4096
  temperature: 0.3         # Lower for consistency
  timeout: 30
  
  # Caching
  cache_enabled: true
  cache_ttl: 3600
```

#### CLI Configuration
```bash
# Set Kimic as default model
opencode config set model nvidia-kimic-2.6

# Set API endpoint
opencode config set model-endpoint http://localhost:8000

# Set API key (if using cloud)
opencode config set nvidia-api-key $NVIDIA_API_KEY

# Verify configuration
opencode config show
```

### Using Kimic with OpenCode

#### Basic Analysis with Kimic
```bash
# Analyze code using Kimic
opencode analyze ./src --model kimic-2.6

# Generate tests with Kimic
opencode generate-tests --model kimic-2.6 ./src

# Document code with Kimic
opencode generate-docs --model kimic-2.6 ./src

# Security scan with Kimic
opencode security-scan --model kimic-2.6 ./src
```

#### Kimic-Specific Features
```bash
# Deep code review
opencode review --deep --model kimic-2.6 ./code.py

# Optimization suggestions
opencode optimize --model kimic-2.6 ./performance-critical.js

# Refactoring recommendations
opencode refactor --ai-model kimic-2.6 ./legacy-code.py

# Generate architecture documentation
opencode document-architecture --model kimic-2.6
```

### Python Integration

#### Use Kimic Directly
```python
from opencode import OpenCodeAnalyzer
from opencode.models import KimicModel

# Initialize Kimic model
kimic = KimicModel(
    base_url="http://localhost:8000",
    model="kimic-2.6"
)

# Initialize analyzer with Kimic
analyzer = OpenCodeAnalyzer(model=kimic)

# Analyze code
results = analyzer.analyze("./src")

# Get recommendations
recommendations = analyzer.get_optimizations()
```

#### Advanced Usage
```python
import requests

# Direct API call to local Kimic
payload = {
    "prompt": "Analyze this code for security vulnerabilities: ...",
    "max_tokens": 2048,
    "temperature": 0.3
}

response = requests.post(
    "http://localhost:8000/v1/completions",
    json=payload
)

analysis = response.json()["choices"][0]["text"]
print(analysis)
```

## Configuration Guide

### Model Parameters Explained

```yaml
# Token management
max_tokens: 4096           # Max response length
context_window: 4096       # Input context size

# Quality tuning
temperature: 0.3           # Lower = more focused (0-1)
top_p: 0.95                # Nucleus sampling
top_k: 50                  # Limit top-k tokens
frequency_penalty: 0       # Repeat penalty
presence_penalty: 0        # New topic penalty

# Performance
timeout: 30                # Request timeout (seconds)
batch_size: 8              # Parallel requests
num_workers: 4             # Worker threads

# Resource management
gpu_memory: auto           # GPU memory allocation
cpu_threads: 4             # CPU thread count
cache_size: 2GB            # Result cache size
```

### Optimal Settings by Use Case

#### Code Generation
```yaml
temperature: 0.2           # Focused, deterministic
max_tokens: 2048           # Enough for functions
top_p: 0.9
```

#### Code Analysis
```yaml
temperature: 0.1           # Very focused
max_tokens: 4096           # Detailed analysis
top_p: 0.95
```

#### Creative Refactoring
```yaml
temperature: 0.7           # More creative
max_tokens: 2048           # Consider multiple approaches
top_p: 0.9
```

### Environment Variables

```bash
# Model configuration
export NVIDIA_KIMIC_MODEL=kimic-2.6
export NVIDIA_KIMIC_ENDPOINT=http://localhost:8000
export NVIDIA_API_KEY=your_key

# Performance tuning
export KIMIC_MAX_TOKENS=4096
export KIMIC_TEMPERATURE=0.3
export KIMIC_BATCH_SIZE=8

# Resource limits
export KIMIC_GPU_MEMORY=8GB
export KIMIC_TIMEOUT=30
export KIMIC_CACHE_SIZE=2GB
```

## Usage & Features

### Code Analysis Examples

#### Analyze Python File
```bash
opencode analyze ./utils.py --model kimic-2.6 --format json > analysis.json

# View results
cat analysis.json | jq '.issues[] | select(.severity=="high")'
```

#### Batch Analysis
```bash
# Analyze entire project
opencode analyze ./src --recursive --model kimic-2.6

# Export report
opencode report --format markdown > code-analysis.md
```

#### Real-time Analysis
```bash
# Watch mode - analyze on file changes
opencode watch ./src --model kimic-2.6

# With auto-fix
opencode watch ./src --auto-fix --model kimic-2.6
```

### Test Generation

#### Generate Tests for Function
```python
# Original function in mycode.py
def calculate_fibonacci(n):
    if n <= 1:
        return n
    return calculate_fibonacci(n-1) + calculate_fibonacci(n-2)
```

```bash
# Generate tests
opencode generate-tests mycode.py --model kimic-2.6

# Output: mycode_test.py with comprehensive test cases
```

#### Generated Tests
```python
import pytest
from mycode import calculate_fibonacci

class TestFibonacci:
    def test_zero(self):
        assert calculate_fibonacci(0) == 0
    
    def test_one(self):
        assert calculate_fibonacci(1) == 1
    
    def test_sequence(self):
        assert calculate_fibonacci(5) == 5
        
    def test_negative(self):
        with pytest.raises(RecursionError):
            calculate_fibonacci(-1)
```

### Documentation Generation

```bash
# Generate comprehensive docs
opencode generate-docs ./src --model kimic-2.6

# Generate API documentation
opencode generate-api-docs ./api --format openapi

# Generate README
opencode generate-readme --model kimic-2.6
```

### Security Scanning

```bash
# Detect vulnerabilities
opencode security-scan ./src --model kimic-2.6

# OWASP Top 10 check
opencode security-scan --owasp-top-10 ./src

# Generate security report
opencode security-report --format pdf > security-audit.pdf
```

## API Integration

### REST API Endpoints

```bash
# Health check
curl http://localhost:8000/health

# Model info
curl http://localhost:8000/v1/models

# Completions
curl -X POST http://localhost:8000/v1/completions \
  -H "Content-Type: application/json" \
  -d '{
    "model": "kimic-2.6",
    "prompt": "def hello(): ",
    "max_tokens": 100
  }'

# Chat completions
curl -X POST http://localhost:8000/v1/chat/completions \
  -H "Content-Type: application/json" \
  -d '{
    "model": "kimic-2.6",
    "messages": [
      {"role": "user", "content": "Explain this code..."}
    ]
  }'
```

### Python SDK

```python
from openai import OpenAI  # Compatible client

# Connect to local Kimic
client = OpenAI(
    api_key="not-needed-for-local",
    base_url="http://localhost:8000/v1"
)

# Generate code
completion = client.completions.create(
    model="kimic-2.6",
    prompt="def sort_array(arr):\n    ",
    max_tokens=200
)

print(completion.choices[0].text)
```

### Docker Compose for OpenCode + Kimic

```yaml
version: '3.8'

services:
  kimic:
    image: nvcr.io/nvidia/kimic:2.6-latest
    ports:
      - "8000:8000"
    environment:
      - NVIDIA_VISIBLE_DEVICES=all
    deploy:
      resources:
        reservations:
          devices:
            - driver: nvidia
              count: 1
              capabilities: [gpu]
  
  opencode:
    image: opencode:latest
    ports:
      - "8080:8080"
    environment:
      - KIMIC_ENDPOINT=http://kimic:8000
      - KIMIC_MODEL=kimic-2.6
    depends_on:
      - kimic
    volumes:
      - ./src:/workspace/src

volumes:
  kimic-cache:
```

## Performance Optimization

### GPU Acceleration

```bash
# Check GPU availability
kimic check-gpu

# Use specific GPU
kimic serve --device cuda:0

# Multi-GPU setup
kimic serve --device cuda:0,cuda:1 --distributed
```

### Quantization (Reduce Memory)

```bash
# Download quantized version (8-bit)
kimic download --model kimic-2.6-q8

# Or 4-bit
kimic download --model kimic-2.6-q4

# Use quantized model
opencode config set model kimic-2.6-q8
```

### Caching Strategy

```yaml
# In opencode.yml
caching:
  enabled: true
  ttl: 3600           # Cache 1 hour
  max_size: 2GB
  strategy: lru       # Least recently used
  
# Specific file caching
cache_patterns:
  - '*.js'
  - '*.py'
  - '*.java'
```

### Batch Processing

```bash
# Process multiple files efficiently
opencode batch-analyze \
  --pattern "**/*.js" \
  --model kimic-2.6 \
  --parallel 4        # 4 parallel processes

# Stream results
opencode stream-analyze ./large-project --model kimic-2.6
```

### Memory Management

```bash
# Monitor memory usage
kimic monitor --interval 5

# Limit memory usage
export KIMIC_MAX_MEMORY=8GB
kimic serve --model kimic-2.6 --max-memory 8GB

# Enable swap if needed
kimic serve --model kimic-2.6 --enable-swap
```

## Troubleshooting

### Connection Issues

```bash
# Test Kimic connection
opencode test-model-connection

# Check endpoint health
curl http://localhost:8000/health

# Verify API key (cloud)
opencode verify-api-key nvidia
```

### Performance Issues

```bash
# Profile performance
kimic profile --model kimic-2.6

# Identify bottlenecks
kimic profile --detailed > performance-report.txt

# Optimize settings
kimic optimize-config
```

### Memory Issues

```bash
# Check available memory
kimic check-memory

# Reduce model size
kimic download --model kimic-2.6-lite

# Enable memory optimization
export PYTORCH_CUDA_ALLOC_CONF=max_split_size_mb:512
kimic serve --memory-efficient
```

### API Errors

```bash
# Enable debug logging
export KIMIC_DEBUG=1
opencode analyze ./src --model kimic-2.6 --verbose

# View logs
kimic logs --tail 100

# Common errors:
# 502: Model overloaded → reduce batch_size
# 504: Timeout → increase timeout
# 429: Rate limited → use local deployment
```

### Rebuild/Reinstall

```bash
# Clear cache
kimic cache-clear

# Reinstall model
pip uninstall nvidia-kimic
pip install --upgrade nvidia-kimic

# Redownload model weights
kimic download --model kimic-2.6 --force
```

## Usage Tips & Best Practices

### Cost Optimization (It's Free!)
```
✓ Use local deployment to eliminate any limits
✓ Enable caching to reuse results
✓ Batch similar tasks together
✓ Use quantized models for faster inference
✓ Schedule heavy analysis off-peak
```

### Quality Tips
```
✓ Lower temperature (0.1-0.3) for code generation
✓ Use context around code for better analysis
✓ Iterative refinement for complex tasks
✓ Validate Kimic suggestions before applying
```

### Integration Tips
```
✓ Use as default model after setup
✓ Integrate in CI/CD pipelines
✓ Monitor performance metrics
✓ Set up auto-scaling if using multi-GPU
✓ Create custom rules for your codebase
```

## Additional Resources

### Links
- NVIDIA Kimic: https://nvidia.com/ai/kimic
- NVIDIA GPU Cloud: https://ngc.nvidia.com
- OpenCode Docs: https://opencode.docs/
- Community Forum: https://forums.nvidia.com

### Getting Help
- NVIDIA Support: support@nvidia.com
- OpenCode Community: https://opencode.community
- GitHub Issues: https://github.com/NVIDIA/Kimic/issues
- Stack Overflow: Tag [nvidia-kimic]

## Complete Setup Checklist

```
□ NVIDIA account created
□ API key generated (if using cloud)
□ Python 3.10+ installed
□ Docker installed (optional)
□ CUDA installed (optional)
□ Kimic downloaded/pulled
□ Environment variables set
□ OpenCode configured
□ Connection tested
□ Model parameters tuned
□ First analysis run successfully
□ Integration with CI/CD setup
```
