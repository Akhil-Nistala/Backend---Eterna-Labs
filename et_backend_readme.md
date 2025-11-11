# Real-Time Aggregator Backend - Eterna Labs

This project is a backend service built using Node.js, Express.js, and TypeScript.  
It aggregates token data from public APIs like DexScreener and Jupiter, and exposes them through a REST API and WebSocket server.

---

## Features

1. Fetches real-time token data from multiple sources.
2. Merges and caches the results to improve performance.
3. Provides REST API and WebSocket endpoints.
4. Handles rate limits, retries, and network errors.
5. Can run with or without Redis (falls back to in-memory cache).

---

## Tech Stack

- Node.js  
- Express.js  
- TypeScript  
- Axios  
- Redis (optional)  
- Jest for testing

---
```
## Structure
real-time-aggregator/
│
├── src/
│   ├── aggregator.ts         -> Core logic to fetch and merge token data
│   ├── cache.ts              -> Cache layer using Redis or in-memory storage
│   ├── routes/
│   │   └── tokens.ts         -> REST API route for /tokens endpoint
│   ├── websocket.ts          -> WebSocket setup for live token updates
│   ├── index.ts              -> Application entry point
│   └── server.ts             -> Express server setup
│
├── tests/                    -> Jest unit and integration tests
├── package.json              -> Project dependencies and scripts
├── tsconfig.json             -> TypeScript configuration
└── README.md                 -> Project documentation
```


---

## Installation

1. Clone this repository:
   git clone https://github.com/Akhil-Nistala/real-time-aggregator.git
   cd real-time-aggregator

2. Install dependencies:
   npm install

3. Build the TypeScript code:
   npm run build

4. Run the server:
   npm start

To run in development mode:
   npm run dev

---

## API Endpoints

### 1. Health Check
GET /
Response:
{
  "ok": true,
  "service": "real-time-aggregator"
}

### 2. Get Aggregated Tokens
GET /tokens
Response:
{
  "data": [
    {
      "symbol": "SOL",
      "priceUsd": 164.12,
      "source": "DexScreener",
      "lastUpdated": 1762855893116
    }
  ]
}

---

## WebSocket

Connect to:
ws://localhost:4000/ws

Receives messages in real time when token prices update.

Example:
{
  "event": "token_update",
  "data": {
    "symbol": "SOL",
    "priceUsd": 164.3
  }
}

---

## Testing

Run the unit and integration tests:
npm test

---

## Author

Name: Akhil Nistala  
Email: akhilnistalaiith@gmail.com  
GitHub: https://github.com/Akhil-Nistala  

---

## Notes

- This project was developed as part of the Eterna Labs Backend Internship Assessment.
- Data is fetched from public APIs:
  - DexScreener: https://api.dexscreener.com/latest/dex/search?q=SOL
  - Jupiter: https://price.jup.ag/v4/price?ids=SOL
- Rate limits may apply depending on the API.

