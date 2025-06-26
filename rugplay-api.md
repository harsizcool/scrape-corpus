# RugPlay API
Here's the RugPlay.com API as text.

API Documentation

Authentication
Include your API key in the Authorization header for all requests:

Authorization: Bearer rgpl_your_api_key

Get Top Coins
GET /api/v1/top

Returns the top 50 coins by market cap.

Endpoint
GET https://rugplay.com/api/v1/top
Example Response
```{
  "coins": [
    {
      "symbol": "TEST",
      "name": "Test",
      "icon": "coins/test.webp",
      "price": 76.52377103,
      "change24h": 7652377003.1039,
      "marketCap": 76523771031.04,
      "volume24h": 13744958.18
    }
  ]
}
```
Get Market Data
GET /api/v1/market

Returns paginated market data with filtering and sorting options.

Endpoint
GET https://rugplay.com/api/v1/market
Query Parameters
search - Search by coin name or symbol
sortBy - Sort field: marketCap, currentPrice, change24h, volume24h, createdAt (default: marketCap)
sortOrder - Sort order: asc, desc (default: desc)
priceFilter - Price range: all, under1, 1to10, 10to100, over100 (default: all)
changeFilter - Change filter: all, gainers, losers, hot, wild (default: all)
page - Page number (default: 1)
limit - Items per page, max 100 (default: 12)
Example Response
```{
  "coins": [
    {
      "symbol": "TEST",
      "name": "Test",
      "icon": "coins/test.webp",
      "currentPrice": 76.52377103,
      "marketCap": 76523771031.04,
      "volume24h": 13744958.18,
      "change24h": 7652377003.1039,
      "createdAt": "2025-06-24T16:18:51.278Z",
      "creatorName": "FaceDev"
    }
  ],
  "total": 150,
  "page": 1,
  "limit": 12,
  "totalPages": 13
}
```
Get Coin Details
GET /api/v1/coin/{symbol}

Returns detailed information about a specific coin including price history.

Endpoint
GET https://rugplay.com/api/v1/coin/{symbol}
Parameters
symbol - Coin symbol (e.g., "TEST")
timeframe - Optional. Chart timeframe: 1m, 5m, 15m, 1h, 4h, 1d (default: 1m)
Example Response
```
{
  "coin": {
    "id": 2668,
    "name": "Test",
    "symbol": "TEST",
    "icon": "coins/test.webp",
    "currentPrice": 76.70938996,
    "marketCap": 76709389959.04,
    "volume24h": 13764558.38,
    "change24h": 7670938895.9045,
    "poolCoinAmount": 114176.23963001,
    "poolBaseCurrencyAmount": 8758389.68983547,
    "circulatingSupply": 1000000000,
    "initialSupply": 1000000000,
    "isListed": true,
    "createdAt": "2025-06-24T16:18:51.278Z",
    "creatorId": 1,
    "creatorName": "FaceDev",
    "creatorUsername": "facedev",
    "creatorBio": "the one and only",
    "creatorImage": "avatars/1.jpg"
  },
  "candlestickData": [
    {
      "time": 1750805760,
      "open": 74.96948181,
      "high": 74.96948181,
      "low": 74.96948181,
      "close": 74.96948181
    }
  ],
  "volumeData": [
    {
      "time": 1750805760,
      "volume": 1234.56
    }
  ],
  "timeframe": "1m"
}
```
Get Coin Holders
GET /api/v1/holders/{symbol}

Returns the top 50 holders of a specific coin.

Endpoint
GET https://rugplay.com/api/v1/holders/{symbol}
Parameters
symbol - Coin symbol (e.g., "TEST")
limit - Number of holders to return, max 200 (default: 50)
```
Example Response
{
  "coinSymbol": "TEST",
  "totalHolders": 50,
  "circulatingSupply": 1000000000,
  "poolInfo": {
    "coinAmount": 114176.23963001,
    "baseCurrencyAmount": 8758389.68983547,
    "currentPrice": 76.70938996
  },
  "holders": [
    {
      "rank": 1,
      "userId": 1,
      "username": "facedev",
      "name": "FaceDev",
      "image": "avatars/1.jpg",
      "quantity": 999883146.4679264,
      "percentage": 99.98831464679265,
      "liquidationValue": 4368219.41924125
    }
  ]
}
```
Get Prediction Markets (Hopium)
GET /api/v1/hopium

Returns prediction market questions with pagination and filtering options.

Endpoint
GET https://rugplay.com/api/v1/hopium
Query Parameters
status - Filter by status: ACTIVE, RESOLVED, CANCELLED, ALL (default: ACTIVE)
page - Page number (default: 1)
limit - Items per page, max 100 (default: 20)
```
Example Response
{
  "questions": [
    {
      "id": 101,
      "question": "will elon musk tweet about rugplay?",
      "status": "ACTIVE",
      "resolutionDate": "2025-07-25T10:39:19.612Z",
      "totalAmount": 4007.76,
      "yesAmount": 3634.65,
      "noAmount": 373.11,
      "yesPercentage": 90.69,
      "noPercentage": 9.31,
      "createdAt": "2025-06-25T10:39:19.613Z",
      "resolvedAt": null,
      "requiresWebSearch": true,
      "aiResolution": null,
      "creator": {
        "id": 3873,
        "name": "Eliaz",
        "username": "eluskulus",
        "image": "avatars/102644133851219200932.png"
      },
      "userBets": null
    }
  ],
  "total": 150,
  "page": 1,
  "limit": 20,
  "totalPages": 8
}
```
Get Prediction Market Details
GET /api/v1/hopium/{question_id}

Returns detailed information about a specific prediction market question including recent bets and probability history.

Endpoint
GET https://rugplay.com/api/v1/hopium/{question_id}
Parameters
question_id - Question ID (e.g., 101)
```
Example Response
{
  "question": {
    "id": 101,
    "question": "will elon musk tweet about rugplay?",
    "status": "ACTIVE",
    "resolutionDate": "2025-07-25T10:39:19.612Z",
    "totalAmount": 4007.76,
    "yesAmount": 3634.65,
    "noAmount": 373.11,
    "yesPercentage": 90.69,
    "noPercentage": 9.31,
    "createdAt": "2025-06-25T10:39:19.613Z",
    "resolvedAt": null,
    "requiresWebSearch": true,
    "aiResolution": null,
    "creator": {
      "id": 3873,
      "name": "Eliaz",
      "username": "eluskulus",
      "image": "avatars/102644133851219200932.png"
    },
    "userBets": null,
    "recentBets": [
      {
        "id": 8066,
        "side": true,
        "amount": 3.84,
        "createdAt": "2025-06-25T14:59:54.201Z",
        "user": {
          "id": 5332,
          "name": "Spam email inhaler",
          "username": "sunny_tiger7616",
          "image": "avatars/111376429189149628011.webp"
        }
      }
    ]
  },
  "probabilityHistory": [
    {
      "time": 1750805760,
      "value": 50.0
    },
    {
      "time": 1750805820,
      "value": 65.2
    }
  ]
}
```
Rate Limiting
• Daily limit: 2,000 requests per day
• Cost: 1 credit per API call
• Error response: 429 Too Many Requests when limit exceeded
• Reset: Daily limits reset every 24 hours

Error Responses
Common Error Codes
```
• 400 - Bad Request (invalid parameters)
• 401 - Unauthorized (invalid or missing API key)
• 404 - Not Found (coin/question doesn't exist)
• 429 - Too Many Requests (rate limit exceeded)
• 500 - Internal Server Error
```
