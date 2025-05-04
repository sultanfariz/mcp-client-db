# ADK Agent with MCP Database Tool

This project demonstrates an AI agent built using the Google Agent Development Kit (ADK) that interacts with a database through a Model Context Protocol (MCP) server. The agent translates natural language requests into SQL queries.

## Prerequisites

*   Python 3.x
*   Node.js (for running the MCP server)
*   pip (Python package installer)
*   Access to a database (the specific type depends on your `DATABASE_URI`)

## Installation

1.  **Clone the repository (if applicable):**
    ```bash
    git clone <repository-url>
    cd <repository-directory>
    ```

2.  **Set up Python Environment:**
    It's recommended to use a virtual environment:
    ```bash
    python3 -m venv .venv
    source .venv/bin/activate # On Windows use `.venv\Scripts\activate`
    ```

3.  **Install Python Dependencies:**
    ```bash
    pip install google-adk python-dotenv
    ```
    *(Add any other Python dependencies if needed)*

4.  **Set up MCP Server:**
    This project assumes you have a separate Node.js-based MCP server. You need to build it and note the path to its main executable (e.g., `index.js` or similar).
    *(Add specific instructions here if the MCP server code is part of this repo and needs building, e.g., `npm install`, `npm run build`)*

## Configuration

1.  **Create Environment File:**
    Copy the example environment file:
    ```bash
    cp .env.example .env
    ```

2.  **Edit `.env`:**
    Open the `.env` file and set the following variables:
    *   `DATABASE_URI`: Your database connection string (e.g., `postgresql://user:password@host:port/database`).
    *   `GOOGLE_API_KEY`: Your Google AI API key. Obtain this from Google Vertex or AI Studio and ensure the Gemini APIs are enabled for your project.
    *   *(Potentially add API keys if the agent uses other services)*

3.  **Update Agent Script:**
    Open `multi_tool_agent/agent.py` and update the path to your MCP server executable in the `StdioServerParameters` section. **Replace `/path/to/build/index.js` with the actual path to your built MCP server script.**
    ```python
    # multi_tool_agent/agent.py
    ...
    StdioServerParameters(
        command='node',
        args=[
          "/path/to/build/index.js",    # <-- IMPORTANT: UPDATE THIS PATH
          os.environ.get("DATABASE_URI")
        ]
      )
    ...
    ```

## Running the Application

1.  **Start the MCP Server:**
    The Python agent script will start the MCP server automatically when it runs, using the command specified in `agent.py`. Ensure Node.js is in your system's PATH and the path in `agent.py` is correct.

2.  **Run the Python Agent:**
    Make sure your virtual environment is activated (`source .venv/bin/activate`).
    Navigate to the root directory of this project (`mcp-client-adk copy`) in your terminal.
    ```bash
    adk web
    ```
    The agent will attempt to connect to the MCP server and become ready to process requests based on its instructions.
