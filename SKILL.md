---
name: hevy
description: Query Hevy workout data via API. View workouts, exercises, routines, and training progress.
---

# Hevy

Access Moritz' training data from Hevy.

## Auth

API key stored in `~/.openclaw/secrets/hevy.env`. All requests need header `api-key: $HEVY_API_KEY`.

## Base URL

`https://api.hevyapp.com/v1`

## Endpoints

### Workouts (paginated)
```bash
source ~/.openclaw/secrets/hevy.env
curl -s -H "api-key: $HEVY_API_KEY" "https://api.hevyapp.com/v1/workouts?page=1&pageSize=5"
```
Returns: `page`, `page_count`, `workouts[]` with exercises and sets.

### Single Workout
```bash
curl -s -H "api-key: $HEVY_API_KEY" "https://api.hevyapp.com/v1/workouts/{workoutId}"
```

### Workout Count
```bash
curl -s -H "api-key: $HEVY_API_KEY" "https://api.hevyapp.com/v1/workouts/count"
```

### Routines
```bash
curl -s -H "api-key: $HEVY_API_KEY" "https://api.hevyapp.com/v1/routines?page=1&pageSize=5"
```

### Exercise Templates
```bash
curl -s -H "api-key: $HEVY_API_KEY" "https://api.hevyapp.com/v1/exercise_templates?page=1&pageSize=10"
```

### Workout Events (since timestamp)
```bash
curl -s -H "api-key: $HEVY_API_KEY" "https://api.hevyapp.com/v1/workouts/events?since=2026-01-01T00:00:00Z&page=1&pageSize=5"
```

## Data Format

Each workout contains:
- `title`: Workout name (e.g. "Oberkörper", "Unterkörper")
- `start_time` / `end_time`: ISO timestamps
- `exercises[]`: Array of exercises, each with:
  - `title`: Exercise name
  - `notes`: User notes
  - `sets[]`: Array with `weight_kg`, `reps`, `rpe`, `distance_meters`, `duration_seconds`

## Routines

- *Oberkörper*: Pull Ups, Dips, Rows, Incline Bench, OHP, Lateral Raise, Bench Machine, Preacher Curl
- *Unterkörper*: Deadlift, Squat Machine, Reverse Lunge, Leg Curl, Leg Extension, Calf Raises, Abs

## Notes

- Weights are always in kg
- Pagination: `page` (1-indexed), `pageSize` (max probably 10)
- All timestamps in ISO 8601
