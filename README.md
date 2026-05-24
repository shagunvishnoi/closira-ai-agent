# Closira AI Engineering Assignment

This project implements an AI-powered customer support workflow for **Bloom Aesthetics Clinic**. The system handles FAQ answering, lead qualification, escalation detection, and conversation summarization.

## Features
- **Grounded FAQ**: Uses a provided SOP (`sop.json`) as the single source of truth.
- **Lead Qualification**: Naturally collects treatment interest, experience, and availability.
- **Escalation Detection**: Monitors for complaints, medical questions, pricing negotiations, and more.
- **Session Summary**: Generates a structured report after each conversation.
- **Hallucination Prevention**: Strict system prompt constraints to stay within SOP boundaries.

## Project Structure
- `main.py`: The core Python workflow implementing the multi-stage logic.
- `sop.json`: The SOP data file for Bloom Aesthetics Clinic.
- `prompt_design.md`: Documentation of prompt strategies and design decisions.
- `test_transcripts/`: Sample conversations demonstrating expected behaviors.
- `escalation_log.json`: (Generated) Log file for triggered escalations.

## Setup Instructions

1. **Clone the repository**:
   ```bash
   git clone <repo-url>
   cd closira-ai-agent
   ```

2. **Set up virtual environment** (optional but recommended):
   ```bash
   python3 -m venv venv
   source venv/bin/activate
   ```

3. **Install dependencies**:
   ```bash
   pip install -r requirements.txt
   ```

4. **Configure environment variables**:
   Create a `.env` file in the root directory and add your API key:
   ```env
   # Choose one or both. If OPENAI_API_KEY is present, it will be used by default.
   GEMINI_API_KEY=your_gemini_key_here
   OPENAI_API_KEY=your_openai_key_here
   ```

## How to Run

Run the main script to start an interactive conversation:
```bash
python main.py
```

### Commands:
- `exit` or `quit`: Ends the session and generates the final summary.
- `summary`: Generates an interim summary of the conversation so far.

## Known Limitations

1. **Gemini vs OpenAI/Claude**: While the assignment specifies OpenAI or Claude, Gemini is used by default for the prototype due to its accessible free tier. The system maintains full model-agnosticism and supports OpenAI via `.env` configuration.
2. **No Persistent Storage**: Conversation history and lead data live in-memory and are reset when the session ends.
3. **API Rate Limits**: The free tier of Gemini has strict limits. The code implements automatic retries and model fallback (2.0, 2.5, 3.1) to mitigate this.
4. **Sentiment Detection**: Relies on the LLM's understanding of context, which may occasionally miss very subtle frustration or sarcasm.
5. **Session-Based Leads**: Lead data is extracted on-the-fly. For a production system, this would be tied to a database like MongoDB or PostgreSQL.
