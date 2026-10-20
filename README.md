# LangGraph Refund Agent

An AI-powered customer refund support system built with FastAPI, LangGraph, and Groq. The application processes customer refund requests, retrieves order information, evaluates refund eligibility, and supports human review for requests that require approval.

## Overview

The LangGraph Refund Agent provides a customer support workflow for handling refund-related queries. It combines a web dashboard with an API backend and an AI-powered agent to classify requests, evaluate outcomes, and generate customer-friendly responses.

The project is designed as a demonstration of AI agents, workflow orchestration, and human-in-the-loop decision-making.

## Features

- **AI-Powered Request Classification:** Identifies customer support intent and extracts order IDs from messages.
- **Order Management:** Retrieves order information through the application database.
- **Refund Decision Workflow:** Processes requests according to the project's refund rules.
- **Human-in-the-Loop Review:** Supports approval or rejection of requests that require manual review.
- **Customer Response Generation:** Generates clear and courteous responses using a Groq-hosted language model.
- **Interactive Dashboard:** Provides order information, request submission, activity logs, and agent results.
- **REST API:** Exposes endpoints for customer support requests, order retrieval, and review decisions.
- **Environment-Based Configuration:** Keeps API credentials separate from application code.

## Tech Stack

- Python
- FastAPI
- LangGraph
- LangChain
- Groq API
- Pydantic
- Uvicorn
- HTML, CSS, and JavaScript

## Project Structure

```text
langgraph-refund-agent/
├── main.py
├── agents.py
├── graph.py
├── database.py
├── schemas.py
├── tools.py
├── requirements.txt
├── .env.example
├── .gitignore
├── README.md
├── data/
└── static/
    ├── index.html
    ├── style.css
    └── script.js
```

The files inside `static/` may have different names depending on your implementation.

## Getting Started

### 1. Clone the Repository

```bash
git clone https://github.com/Rameeshafatima-png/langgraph-refund-agent.git
cd langgraph-refund-agent
```

### 2. Create a Virtual Environment

**Windows PowerShell**

```powershell
python -m venv .venv
.venv\Scripts\Activate.ps1
```

### 3. Install Dependencies

```bash
python -m pip install -r requirements.txt
```

### 4. Configure Environment Variables

Create a `.env` file in the project root:

```env
GROQ_API_KEY=your_groq_api_key
GROQ_MODEL=openai/gpt-oss-120b
```

Replace `your_groq_api_key` with your own valid API key.

Get your API key from the [Groq Console](https://console.groq.com/).

Never commit your `.env` file or expose your API key publicly.

### 5. Run the Application

```bash
uvicorn main:app --reload
```

Open the following URLs in your browser:

- **Dashboard:** http://127.0.0.1:8000/
- **API Documentation:** http://127.0.0.1:8000/docs
- **Health Check:** http://127.0.0.1:8000/health
- **Orders API:** http://127.0.0.1:8000/orders

## API Endpoints

| Method | Endpoint | Description |
|---|---|---|
| GET | `/` | Serves the dashboard |
| GET | `/health` | Checks application health |
| GET | `/orders` | Retrieves available orders |
| POST | `/support` | Submits a customer support request |
| POST | `/review/{thread_id}` | Approves or rejects a pending human review |

Interactive API testing is available through the FastAPI Swagger interface at `/docs`.

## How It Works

1. A customer submits a refund-related message through the dashboard.
2. The AI agent classifies the request and extracts the order ID when available.
3. The workflow retrieves relevant order information and evaluates the request.
4. Requests requiring human review can pause for an approval decision.
5. The workflow resumes after the review decision.
6. The agent generates a customer-friendly response based on the final outcome.

The exact decision rules and workflow transitions are implemented in the project's graph, database, and tool modules.

## Human-in-the-Loop Workflow

Human review allows an eligible workflow to pause until an authorized decision is supplied. LangGraph manages the workflow state, while the application exposes a review endpoint to submit approval or rejection.

The current implementation uses an in-memory checkpointer. Workflow state may not survive application restarts or be shared across independent server instances. Persistent checkpoint storage is recommended for production deployments.

## Configuration

| Variable | Purpose |
|---|---|
| `GROQ_API_KEY` | Authenticates requests to the Groq API |
| `GROQ_MODEL` | Specifies the language model used by the agent |

Ensure that the selected model is available to your Groq account.

## Deployment

The application can be prepared for deployment on a compatible Python hosting platform.

Before deploying:

- Configure environment variables securely.
- Verify that static assets are included in the deployment.
- Confirm that the database supports the chosen hosting environment.
- Configure persistent workflow checkpoint storage if required.
- Test all API endpoints and the human-review workflow.

Vercel supports FastAPI applications, but deployment configuration and database persistence must be verified for this particular project.

## Security Notes

- Keep API keys in environment variables.
- Do not upload `.env` or virtual environment folders to GitHub.
- Validate incoming customer requests.
- Protect review endpoints with authentication and authorization before production use.
- Do not treat a demo database update as proof that a real payment has been issued.

## Future Improvements

- Persistent database and checkpoint storage.
- Authentication and role-based access control.
- Automated testing and improved error handling.
- Refund analytics and reporting.
- Deployment monitoring and structured logging.
- More comprehensive refund policy validation.

## Author

**Rameesha Fatma**

GitHub: [Rameeshafatima-png](https://github.com/Rameeshafatima-png)

## License

This project is intended for educational and portfolio purposes. Add a license file if you want to specify the terms under which others may use or distribute the code.
