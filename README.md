# Multi-LLM Council System

A sophisticated multi-agent AI system that leverages multiple Large Language Models (LLMs) to collaboratively generate, review, and reach consensus on responses, significantly improving reliability and output quality.

## 🌟 Project Overview

The Multi-LLM Council System implements a **democratic approach to AI decision-making** by orchestrating multiple LLMs in a structured workflow. Instead of relying on a single model's output, this system employs:

- **Multiple Generation Agents**: Different LLMs independently generate responses to the same prompt
- **Peer Review Process**: Generated responses are cross-evaluated by other LLMs
- **Consensus Mechanism**: A final arbitrator synthesizes the best elements from all submissions
- **Quality Assurance**: Built-in verification and validation steps ensure coherent, accurate outputs

This approach mirrors real-world expert panels where diverse perspectives lead to more robust conclusions.

## 🚀 How It Works

1. **Input Distribution**: A user query is simultaneously sent to multiple LLM endpoints (Gemini, Ollama models, etc.)

2. **Parallel Generation**: Each LLM generates its own independent response based on the prompt

3. **Cross-Review Phase**: 
   - Each generated response is evaluated by other LLMs in the council
   - Reviews assess accuracy, completeness, clarity, and potential issues
   - Critical feedback is aggregated

4. **Consensus Building**:
   - A designated "council leader" (typically the most capable model) reviews all responses and critiques
   - Synthesizes the strongest points from each submission
   - Produces a final, refined answer incorporating collective wisdom

5. **Output Delivery**: The consensus response is returned to the user with optional metadata about the decision process

## 📊 Architecture

The system is orchestrated using n8n workflows that coordinate API calls, manage data flow, and implement the review logic.

![Architecture Diagram](diagrams/architecture.png)

*The workflow demonstrates parallel LLM invocation, structured review loops, and consensus aggregation.*

## 🎯 Example Output

See our [workflow screenshot](screenshots/workflow.png) for a visual representation of the n8n automation and [sample output](screenshots/output.png) showing the consensus-building process in action.

## 🛠️ Tech Stack

- **Workflow Orchestration**: [n8n](https://n8n.io/) - Open-source workflow automation
- **LLM Providers**:
  - Google Gemini API (Cloud-based, high-capability model)
  - Ollama (Local models for privacy-sensitive tasks)
  - Extensible to OpenAI, Anthropic, or other providers
- **Multi-Agent Architecture**: Custom orchestration pattern implementing council consensus
- **API Integration**: RESTful communication between workflow nodes and LLM endpoints

## 💡 Why This Approach?

### Improved Reliability
- **Error Mitigation**: Single-model hallucinations are caught by peer review
- **Bias Reduction**: Different models have different training data and tendencies
- **Robustness**: System continues functioning even if one LLM endpoint fails

### Enhanced Quality
- **Diverse Perspectives**: Multiple models bring different strengths (creativity, accuracy, reasoning)
- **Validation**: Answers are automatically fact-checked by other LLMs
- **Refinement**: Final output benefits from iterative improvement

### Transparency
- **Traceable Decisions**: Can inspect individual responses and review comments
- **Explainability**: Understand *why* the final answer was chosen
- **Confidence Scoring**: Identify when models disagree (flag for human review)

### Cost Optimization
- **Hybrid Strategy**: Use expensive cloud models alongside free local models
- **Selective Deployment**: Simple queries can bypass full council review
- **Scalability**: Add/remove models based on budget and requirements

## 📦 Getting Started

### Prerequisites
- n8n installed (self-hosted or cloud)
- API keys for cloud LLM providers (Gemini, etc.)
- Ollama running locally (optional, for local models)

### Installation

1. Clone this repository:
   ```bash
   git clone https://github.com/AnshGajera/multi-llm-council.git
   cd multi-llm-council
   ```

2. Import the workflow into n8n:
   - Open n8n interface
   - Go to **Workflows** → **Import from File**
   - Select `workflows/n8n-workflow.json`

3. Configure credentials:
   - Add your Gemini API key in n8n credentials
   - Configure Ollama endpoint (default: http://localhost:11434)
   - Set up any additional LLM provider credentials

4. Activate the workflow and test with a sample query

### Usage

Send a POST request to your n8n webhook URL with:
```json
{
  "query": "Your question here",
  "context": "Optional context information"
}
```

The system will return a consensus response along with metadata about the council's decision process.

## 📁 Repository Structure

```
multi-llm-council/
├── workflows/          # n8n workflow definitions
├── diagrams/           # Architecture diagrams and flowcharts
├── screenshots/        # Workflow and output examples
├── README.md           # This file
└── LICENSE             # MIT License
```

## 🤝 Contributing

Contributions are welcome! Whether you want to:
- Add support for new LLM providers
- Improve the consensus algorithm
- Enhance error handling
- Share example use cases

Please feel free to open issues or submit pull requests.

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- Built with [n8n](https://n8n.io/) - the workflow automation platform
- Powered by Google Gemini, Ollama, and the open-source AI community
- Inspired by ensemble methods in machine learning and democratic decision-making processes

---

**Note**: This is an experimental project demonstrating multi-agent AI orchestration. For production use, consider implementing additional security measures, rate limiting, and cost controls.
