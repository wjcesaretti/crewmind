# CrewMind - Smart Lineup Optimizer

This project is an AI system designed to predict fast rowing lineups and ensure they adhere to team rules, side preferences, and safety standards.

## Project Structure

```
crewmind/
├── api/
│   └── main.py               # FastAPI application
├── ml_model/
│   └── predict_lineup.py     # Mock ML model for lineup prediction
├── ontology/
│   └── crew_validator.py     # Python-based lineup validation logic
├── data/                     # Directory for CSV data files
│   ├── rowers.csv
│   ├── seats.csv
│   └── past_lineups.csv
├── README.md                 # This file
└── requirements.txt          # Python package dependencies
```

## Setup

1.  **Clone the repository (if applicable)**
2.  **Create a virtual environment (recommended):**
    ```bash
    python -m venv venv
    source venv/bin/activate  # On Windows: venv\Scripts\activate
    ```
3.  **Install dependencies:**
    ```bash
    pip install -r requirements.txt
    ```
4.  **Run the FastAPI application:**
    ```bash
    uvicorn api.main:app --reload --port 8000
    ```
    The API will be available at `http://localhost:8000`.

## Usage

Send a POST request to the `/lineup/suggest` endpoint with a JSON payload describing the available rowers.

**Example Request:**
```json
{
  "rowers": [
    {"id": "r1", "name": "Alice", "erg_score": 480, "side_pref": "port", "weight": 70, "experience": 3, "back_injury": false},
    {"id": "r2", "name": "Bob", "erg_score": 470, "side_pref": "starboard", "weight": 75, "experience": 2, "back_injury": false},
    {"id": "r3", "name": "Charlie", "erg_score": 490, "side_pref": "any", "weight": 68, "experience": 4, "back_injury": true},
    {"id": "r4", "name": "Diana", "erg_score": 460, "side_pref": "port", "weight": 72, "experience": 1, "back_injury": false}
    // ... add more rowers for an 8-person boat + coxswain if needed
  ],
  "boat_type": "8+" // or "4+", "2x", etc.
}
```

**Example Response:**
```json
[
  {
    "lineup": ["r1", "r2", ...], // List of rower IDs in seat order
    "predicted_speed": 6.02,
    "valid": true,
    "issues": []
  },
  // ... other suggested lineups
]
``` 