# VALIDATE.AI API Documentation

## POST /api/ideas
Submits a new startup idea for validation. Returns a 202 Accepted status with a polling URL.

**Request Body:**
```json
{
  "title": "Uber for Dog Walking",
  "description": "A platform connecting dog owners with local, vetted dog walkers on demand.",
  "persona": "Investor", // Optional: "Investor", "Architect", "Futurist". Defaults to "Investor".
  "tags": ["pets", "marketplace"] // Optional
}
```

**Successful Response (202 Accepted):**
```json
{
  "message": "Idea received. Generation enqueued.",
  "ideaId": "550e8400-e29b-41d4-a716-446655440000",
  "pollUrl": "/api/ideas/550e8400-e29b-41d4-a716-446655440000"
}
```

**Cached Response (200 OK):**
```json
{
  "message": "Found cached critique.",
  "ideaId": "550e8400-e29b-41d4-a716-446655440000",
  "pollUrl": "/api/ideas/550e8400-e29b-41d4-a716-446655440000"
}
```

---

## GET /api/ideas/:id
Polls for the status and result of an idea validation. 

**Response (Pending 200 OK):**
```json
{
  "idea": {
    "id": "...",
    "title": "...",
    "status": "pending",
    "persona": "Investor"
  },
  "critique": null
}
```

**Response (Completed 200 OK):**
```json
{
  "idea": {
    "id": "...",
    "status": "completed"
  },
  "critique": {
    "summary": "High margin but operationally intense.",
    "points": [
      {
        "title": "Market Size is Niche",
        "detail": "While pet ownership is high, paying for premium on-demand walking is limited to dense urban areas.",
        "tags": ["market"]
      }
    ],
    "tone": "brutal-but-fair",
    "confidence_score": 0.85
  }
}
```
