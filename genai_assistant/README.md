# Boston 311 GenAI Intake Assistant

This component uses retrieval-augmented generation and structured model output
to classify resident messages by Boston 311 request type, department, and queue.
It can also ask a follow-up question when a resident's message does not contain
enough information for reliable routing.

## Files

- `notebooks/Boston_311_Intake_Assistant.ipynb` — assistant implementation,
  demonstrations, and evaluation.
- `results/intake_tests.csv` — results for 35 evaluation messages.
- `results/reference_list.csv` — generated locally when the notebook runs.

## Evaluation

The submitted notebook reports:

- Request-type accuracy: 96.8%
- Department accuracy: 96.8%
- Unnecessary follow-up questions on clear messages: 0 out of 31

## Setup

Install the project dependencies from the repository root:

```bash
python -m pip install -r requirements.txt
```

Place both raw Boston 311 CSV files in `data/raw/`, as described in
`data/raw/README.md`.

Set the API key in your terminal before opening the notebook:

```bash
export OPENAI_API_KEY="your-api-key"
```

Do not commit an actual API key or `.env` file to GitHub.

Run `notebooks/Boston_311_Intake_Assistant.ipynb` from the repository root or
from its notebook directory. Generated evaluation artifacts are written to
`genai_assistant/results/`.

## Models Used

- `gpt-4o-mini` for structured classification
- `text-embedding-3-small` for reference-list retrieval

## Limitations

The assistant depends on the historical request types and queues in the source
data. New or rare request types may require additional examples or updates to
the reference list. Production use would also require monitoring, privacy
controls, human escalation, and periodic evaluation.
