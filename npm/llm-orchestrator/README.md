<div align="center">

# LLM Orchestrator

<p align="center">
  <strong>Production-ready LLM workflow orchestrator with DAG execution, state management, and multi-provider support</strong>
</p>

<p align="center">
  <a href="https://www.npmjs.com/package/@llm-dev-ops/llm-orchestrator"><img src="https://img.shields.io/npm/v/@llm-dev-ops/llm-orchestrator.svg?style=flat-square" alt="npm version"></a>
  <a href="https://www.npmjs.com/package/@llm-dev-ops/llm-orchestrator"><img src="https://img.shields.io/npm/dm/@llm-dev-ops/llm-orchestrator.svg?style=flat-square" alt="npm downloads"></a>
  <a href="https://github.com/globalbusinessadvisors/llm-orchestrator/blob/main/LICENSE"><img src="https://img.shields.io/badge/license-Apache--2.0-blue.svg?style=flat-square" alt="License"></a>
  <a href="https://github.com/globalbusinessadvisors/llm-orchestrator"><img src="https://img.shields.io/github/stars/globalbusinessadvisors/llm-orchestrator.svg?style=flat-square&logo=github" alt="GitHub stars"></a>
  <a href="https://github.com/globalbusinessadvisors/llm-orchestrator/actions"><img src="https://img.shields.io/github/actions/workflow/status/globalbusinessadvisors/llm-orchestrator/ci.yml?style=flat-square" alt="Build Status"></a>
</p>

<p align="center">
  <a href="#-quick-start">Quick Start</a> •
  <a href="#-features">Features</a> •
  <a href="#-installation">Installation</a> •
  <a href="#-examples">Examples</a> •
  <a href="#-documentation">Documentation</a> •
  <a href="#-contributing">Contributing</a>
</p>

</div>

---

## ✨ Features

<table>
<tr>
<td width="50%">

### 🔄 **DAG-Based Execution**
Build complex workflows with automatic dependency resolution and parallel execution. Define once, run efficiently.

### 🎯 **Multi-Provider Support**
Seamlessly integrate OpenAI, Anthropic Claude, Cohere, and custom providers. Switch providers without changing your workflows.

### 💾 **State Management**
Persistent state across runs with intelligent caching. Resume failed workflows from the last successful step.

### 📝 **Templating Engine**
Handlebars-powered dynamic prompts with full access to workflow state, previous outputs, and custom variables.

</td>
<td width="50%">

### 📊 **Observability**
Built-in metrics, distributed tracing, and structured logging. Monitor every step of your LLM workflows.

### 🔒 **Type Safety**
Written in Rust for memory safety and reliability. Zero-cost abstractions with native performance.

### ⚡ **High Performance**
Concurrent execution with configurable parallelism. Process multiple LLM calls simultaneously.

### 🛡️ **Error Handling**
Automatic retry with exponential backoff, circuit breakers, and graceful degradation strategies.

</td>
</tr>
</table>

---

## 🚀 Quick Start

Install globally and run your first workflow in under 60 seconds:

```bash
# Install
npm install -g @llm-dev-ops/llm-orchestrator

# Create a workflow
cat > sentiment.yaml << 'EOF'
name: sentiment-analysis
version: "1.0"

providers:
  openai:
    type: openai
    model: gpt-4

steps:
  - id: analyze
    provider: openai
    prompt: "Analyze sentiment: {{input.text}}"

  - id: classify
    provider: openai
    prompt: "Classify as positive/negative/neutral: {{steps.analyze.output}}"
    depends_on: [analyze]
EOF

# Run it
export OPENAI_API_KEY="sk-..."
llm-orchestrator run sentiment.yaml --input '{"text": "I love this product!"}'
```

---

## 📦 Installation

### NPM (Recommended)

```bash
# Global installation (CLI)
npm install -g @llm-dev-ops/llm-orchestrator

# Local installation (Programmatic API)
npm install @llm-dev-ops/llm-orchestrator
```

### Yarn

```bash
yarn global add @llm-dev-ops/llm-orchestrator
```

### PNPM

```bash
pnpm add -g @llm-dev-ops/llm-orchestrator
```

### Docker

```bash
# Pull the image
docker pull ghcr.io/globalbusinessadvisors/llm-orchestrator:latest

# Run a workflow
docker run -v $(pwd):/workspace \
  -e OPENAI_API_KEY="$OPENAI_API_KEY" \
  ghcr.io/globalbusinessadvisors/llm-orchestrator:latest \
  run /workspace/workflow.yaml
```

### Supported Platforms

| Platform | Architecture | Status |
|----------|-------------|---------|
| 🐧 Linux | x64 | ✅ |
| 🐧 Linux | ARM64 | ✅ |
| 🍎 macOS | Intel | ✅ |
| 🍎 macOS | Apple Silicon | ✅ |

---

## 📚 Examples

### Content Generation Pipeline

```yaml
name: blog-post-generator
version: "1.0"

providers:
  claude:
    type: anthropic
    model: claude-3-5-sonnet-20241022

steps:
  - id: research
    provider: claude
    prompt: |
      Research {{input.topic}} and provide 5 key points.
      Focus on recent developments and practical applications.

  - id: outline
    provider: claude
    prompt: |
      Create a detailed blog post outline about {{input.topic}}.
      Use these key points: {{steps.research.output}}
    depends_on: [research]

  - id: draft
    provider: claude
    prompt: |
      Write a comprehensive blog post following this outline:
      {{steps.outline.output}}

      Tone: {{input.tone}}
      Target audience: {{input.audience}}
    depends_on: [outline]

  - id: edit
    provider: claude
    prompt: |
      Edit and improve this blog post:
      {{steps.draft.output}}

      Focus on clarity, engagement, and SEO optimization.
    depends_on: [draft]
```

**Run it:**

```bash
llm-orchestrator run blog-post.yaml --input '{
  "topic": "AI in Healthcare",
  "tone": "professional",
  "audience": "healthcare executives"
}'
```

### Parallel Data Analysis

```yaml
name: data-analysis
version: "1.0"

providers:
  openai:
    type: openai
    model: gpt-4-turbo

steps:
  # These run in parallel
  - id: sentiment
    provider: openai
    prompt: "Analyze sentiment in: {{input.text}}"

  - id: entities
    provider: openai
    prompt: "Extract named entities from: {{input.text}}"

  - id: keywords
    provider: openai
    prompt: "Extract key topics from: {{input.text}}"

  # This waits for all parallel steps
  - id: summary
    provider: openai
    prompt: |
      Create a comprehensive analysis summary:

      Sentiment: {{steps.sentiment.output}}
      Entities: {{steps.entities.output}}
      Keywords: {{steps.keywords.output}}
    depends_on: [sentiment, entities, keywords]
```

### Multi-Provider Workflow

```yaml
name: multi-provider
version: "1.0"

providers:
  openai:
    type: openai
    model: gpt-4

  claude:
    type: anthropic
    model: claude-3-5-sonnet-20241022

steps:
  - id: brainstorm
    provider: openai
    prompt: "Brainstorm ideas for: {{input.project}}"

  - id: refine
    provider: claude
    prompt: |
      Refine and improve these ideas:
      {{steps.brainstorm.output}}
    depends_on: [brainstorm]

  - id: validate
    provider: openai
    prompt: |
      Validate the feasibility of:
      {{steps.refine.output}}
    depends_on: [refine]
```

---

## 🔧 CLI Reference

### Commands

```bash
# Validate workflow syntax
llm-orchestrator validate <workflow.yaml>

# Run a workflow
llm-orchestrator run <workflow.yaml> [options]

# Options:
#   --input, -i <json>           Input data as JSON string
#   --max-concurrency <number>   Maximum concurrent steps (default: 10)
#   --output, -o <file>          Write output to file
#   --verbose, -v                Enable verbose logging
#   --dry-run                    Validate without executing

# Show version
llm-orchestrator --version

# Show help
llm-orchestrator --help
```

### Environment Variables

```bash
# Provider API Keys
export OPENAI_API_KEY="sk-..."
export ANTHROPIC_API_KEY="sk-ant-..."
export COHERE_API_KEY="..."

# Configuration
export LLM_ORCHESTRATOR_LOG_LEVEL="info"  # debug, info, warn, error
export LLM_ORCHESTRATOR_TIMEOUT="300"     # seconds
export LLM_ORCHESTRATOR_RETRY_MAX="3"     # max retries
```

---

## 💻 Programmatic API

### Basic Usage

```javascript
const orchestrator = require('@llm-dev-ops/llm-orchestrator');

async function main() {
  const result = await orchestrator.run('workflow.yaml', {
    input: JSON.stringify({
      topic: 'AI Ethics',
      depth: 'comprehensive'
    }),
    maxConcurrency: 5,
    verbose: true
  });

  console.log('Output:', result.stdout);
  console.log('Errors:', result.stderr);
  console.log('Exit code:', result.exitCode);
}

main().catch(console.error);
```

### Advanced Usage

```javascript
const { Orchestrator, WorkflowBuilder } = require('@llm-dev-ops/llm-orchestrator');

// Build workflow programmatically
const workflow = new WorkflowBuilder()
  .setName('dynamic-workflow')
  .addProvider('openai', {
    type: 'openai',
    model: 'gpt-4'
  })
  .addStep('analyze', {
    provider: 'openai',
    prompt: 'Analyze: {{input.text}}'
  })
  .build();

// Execute with custom configuration
const orchestrator = new Orchestrator({
  maxConcurrency: 10,
  timeout: 300,
  retries: 3
});

const result = await orchestrator.execute(workflow, {
  text: 'Sample input'
});
```

---

## 🏗️ Workflow Schema

### Complete Workflow Structure

```yaml
name: workflow-name           # Required: Unique workflow identifier
version: "1.0"                # Required: Semantic version

description: |                # Optional: Workflow description
  Detailed description of what this workflow does

providers:                    # Required: At least one provider
  provider-id:
    type: openai|anthropic|cohere|custom
    model: model-name
    api_key: ${ENV_VAR}      # Optional: Override environment variable
    endpoint: https://...     # Optional: Custom endpoint
    temperature: 0.7          # Optional: Provider-specific config
    max_tokens: 2000

steps:                        # Required: At least one step
  - id: step-name            # Required: Unique step identifier
    provider: provider-id     # Required: Reference to provider
    prompt: |                 # Required: Prompt template
      Your prompt here with {{variables}}
    depends_on:               # Optional: Step dependencies
      - previous-step-id
    retry:                    # Optional: Retry configuration
      max_attempts: 3
      backoff: exponential
    timeout: 60               # Optional: Step timeout in seconds
    condition: |              # Optional: Conditional execution
      {{steps.previous.output}} != "skip"
```

---

## 🎯 Use Cases

<table>
<tr>
<td width="50%">

### Content Creation
- Blog post generation
- Social media content
- Marketing copy
- SEO optimization
- Technical documentation

### Data Analysis
- Sentiment analysis
- Entity extraction
- Text classification
- Summarization
- Topic modeling

</td>
<td width="50%">

### Customer Support
- Ticket classification
- Response generation
- FAQ automation
- Escalation detection
- Quality assurance

### Development
- Code review
- Documentation generation
- Test case creation
- Bug report analysis
- API design assistance

</td>
</tr>
</table>

---

## 🔍 Troubleshooting

<details>
<summary><b>Command not found after installation</b></summary>

Ensure npm's global bin directory is in your PATH:

```bash
# Check npm global bin path
npm bin -g

# Add to PATH (add to ~/.bashrc or ~/.zshrc)
export PATH="$(npm bin -g):$PATH"
```
</details>

<details>
<summary><b>API Key errors</b></summary>

Verify your environment variables are set correctly:

```bash
# Check if variables are set
echo $OPENAI_API_KEY
echo $ANTHROPIC_API_KEY

# Ensure they're exported
export OPENAI_API_KEY="sk-..."
```
</details>

<details>
<summary><b>Workflow validation errors</b></summary>

Common issues:
- Missing `depends_on` for steps that reference other steps
- Invalid provider references
- Malformed YAML syntax
- Circular dependencies

Run validation:
```bash
llm-orchestrator validate workflow.yaml
```
</details>

<details>
<summary><b>Performance issues</b></summary>

Optimize your workflows:
- Increase `--max-concurrency` for parallel steps
- Use caching for repeated operations
- Reduce prompt sizes
- Consider using faster models for simple tasks
</details>

---

## 🤝 Contributing

We welcome contributions! Please see our [Contributing Guide](https://github.com/globalbusinessadvisors/llm-orchestrator/blob/main/CONTRIBUTING.md) for details.

### Development Setup

```bash
# Clone the repository
git clone https://github.com/globalbusinessadvisors/llm-orchestrator.git
cd llm-orchestrator

# Install dependencies
cargo build

# Run tests
cargo test

# Run examples
cargo run --example basic-workflow
```

---

## 📄 License

This project is dual-licensed under:

- [MIT License](https://opensource.org/licenses/MIT)
- [Apache License 2.0](https://www.apache.org/licenses/LICENSE-2.0)

You may choose either license for your use.

---

## 💬 Community & Support

- **GitHub Issues**: [Report bugs or request features](https://github.com/globalbusinessadvisors/llm-orchestrator/issues)
- **GitHub Discussions**: [Ask questions and share ideas](https://github.com/globalbusinessadvisors/llm-orchestrator/discussions)
- **Documentation**: [Full documentation](https://github.com/globalbusinessadvisors/llm-orchestrator/wiki)
- **Stack Overflow**: Tag questions with `llm-orchestrator`

---

## 🙏 Acknowledgments

Built with:
- [Rust](https://www.rust-lang.org/) - Systems programming language
- [Tokio](https://tokio.rs/) - Async runtime
- [Handlebars](https://handlebarsjs.com/) - Templating engine
- [Petgraph](https://github.com/petgraph/petgraph) - Graph algorithms

---

<div align="center">

**[⬆ back to top](#llm-orchestrator)**

Made with ❤️ by the LLM DevOps Team

</div>
