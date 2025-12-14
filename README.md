# Plan-and-Execute AI Agent

A sophisticated AI agent built with LangGraph that uses a plan-and-execute architecture to answer complex, multi-step queries. The agent creates a step-by-step plan, executes each step using tools (like web search), and can dynamically re-plan based on intermediate results.

## Features

- **Intelligent Planning**: Creates structured, step-by-step plans to tackle complex queries
- **Tool Execution**: Uses tools (like Tavily web search) to gather information
- **Dynamic Re-planning**: Adapts the plan based on execution results
- **State Management**: Maintains conversation state across planning and execution cycles
- **Robust Error Handling**: Includes fallback mechanisms for handling various response formats

## Architecture

The agent follows a three-stage workflow:

1. **Planning**: Analyzes the user query and creates a structured plan
2. **Execution**: Executes each step in the plan using available tools
3. **Re-planning**: Evaluates results and either continues execution or provides the final answer

```
START → Planner → Executor → Replanner → (Continue/End)
```

## Prerequisites

- Python 3.8 or higher
- API keys for:
  - OpenRouter (for LLM access)
  - Tavily (for web search)

## Installation

1. Clone this repository:
```bash
git clone https://github.com/panditpooja/Plan-and-Execute-AI-Agent.git
```

2. Install dependencies:
```bash
pip install -r requirements.txt
```

3. Set up environment variables:
```bash
cp .env.example .env
```

4. Edit `.env` and add your API keys:
```
OPENROUTER_API_KEY=your_openrouter_api_key_here
TAVILY_API_KEY=your_tavily_api_key_here
```

## Usage

### Running in Jupyter Notebook

1. Open `plan_and_execute_system.ipynb` in Jupyter Notebook or JupyterLab
2. Run all cells to initialize the agent
3. Modify the `user_query` variable in the last cell to ask your question
4. Execute the cell to get results

### Example Query

```python
user_query = "Which country will host the next FIFA World Cup, and what are the top three tourist attractions in its capital city?"
```

## How It Works

### State Management

The agent maintains state across execution cycles:
- `input`: The original user query
- `plan`: List of steps to execute
- `past_steps`: History of completed steps and their results
- `response`: Final answer to the user

### Planning Node

The planner analyzes the query and generates a structured plan with actionable steps. It includes robust error handling to parse various response formats.

### Execution Node

Each step in the plan is executed using an agent that can:
- Use tools (like Tavily web search)
- Process information
- Return results for the next stage

### Re-planning Node

After each execution, the replanner:
- Evaluates the current state
- Decides whether to continue with remaining steps
- Updates the plan if needed
- Provides the final answer when all steps are complete

## Configuration

### Model Configuration

The agent uses OpenRouter's API with the `openai/gpt-oss-120b:free` model. You can modify the model in the notebook:

```python
llm = ChatOpenAI(
    model="openai/gpt-oss-120b:free",  
    base_url="https://openrouter.ai/api/v1",
    api_key=os.getenv("OPENROUTER_API_KEY"),
    temperature=0
)
```

### Tools

Currently, the agent uses:
- **Tavily Search**: For web search capabilities

You can add more tools by extending the `tools` list in the notebook.

## Project Structure

```
Plan-and-Execute-AI-Agent/
├── plan_and_execute_system.ipynb  # Main notebook with agent implementation
├── README.md                       # This file
├── requirements.txt                # Python dependencies
├── .env.example                   # Example environment variables
└── .gitignore                      # Git ignore rules
```

## Dependencies

Key dependencies include:
- `langchain-openai`: OpenAI-compatible LLM integration
- `langchain-tavily`: Tavily search tool integration
- `langgraph`: Graph-based agent orchestration
- `pydantic`: Data validation and settings management
- `python-dotenv`: Environment variable management

See `requirements.txt` for the complete list.

## Limitations

- The agent may require multiple iterations to complete complex queries
- Web search results depend on Tavily API availability
- Model responses may vary based on the LLM provider

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## Acknowledgments

- Built with [LangGraph](https://github.com/langchain-ai/langgraph)
- Uses [LangChain](https://github.com/langchain-ai/langchain) for tool integration
- Powered by [OpenRouter](https://openrouter.ai/) for LLM access
- Uses [Tavily](https://tavily.com/) for web search capabilities

## ✍️ Author

**Pooja Pandit**  
Master's in Information Science (Machine Learning)  
The University of Arizona

[![GitHub](https://img.shields.io/badge/GitHub-panditpooja-black?logo=github)](https://github.com/panditpooja)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-pooja--pandit-blue?logo=linkedin)](https://www.linkedin.com/in/pooja-pandit-177978135/)