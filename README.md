# Fibonacci Sequence Complex App
This application returns the results of the Fibonacci sequence by leveraging an intentionally over-engineered microservices architecture to demonstrate containers connected to one other.

## Architectural Flow
### Step 1
User Web Browser -> Nginx Router
### Step 2
Nginx Router -> React Server -> Express API Server
Nginx Router -> Express API Server

### Step 3
Express API Server -> Redis DB <-> Worker Server
Express API Server -> Postgres DB

## Solution Components
### Nginx Router
Used as a proxy to route traffic to either the React Server or the Express Server for API requests

### React Server
Seres up all web requests for the Fibonacci UI

### Express API Server
Handles all API calls<br />
/ - Returns "Hi" as a test<br />
/values - Receives input from browser<br />
/values/all - queries Postgres DB for all past values searched<br />
/values/current - sends current value to RedisDB

### Redis DB
Stores all indices and calculated values as key-value pairs

### Postgres DB
Stores a permanent list of indicies that have been received

### Worker Server
Watches Redis db for new indicies.  Pulls each new indice, calculates new value hten puts it back into Redis DB.
