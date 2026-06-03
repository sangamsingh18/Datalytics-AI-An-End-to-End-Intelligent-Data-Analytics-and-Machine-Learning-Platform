# DATALYTICS AI - 50 INTERVIEW QUESTIONS
## Comprehensive Interview Guide for Full-Stack Analytics & ML Platform

---

## TABLE OF CONTENTS
1. **Easy Questions (20)** - Project Overview, Features, Tech Stack
2. **Medium Questions (20)** - Architecture, APIs, Performance
3. **Hard Questions (10)** - System Design, Scalability, Production Scenarios

---

# ⭐ EASY QUESTIONS (1-20)

---

## Q1: Project Overview & Purpose
**Difficulty:** Easy  
**Question:** What is Datalytics AI, and what problem does it solve?

**Expected Answer (1-2 minutes):**
Datalytics AI is an end-to-end intelligent data analytics and machine learning platform. The problem it solves is that businesses and data analysts need a single place to:
- Upload data from multiple sources (CSV, Excel, JSON, databases)
- Clean and prepare the data
- Explore and visualize data automatically
- Train ML models without writing code
- Get AI-powered insights and recommendations
- Export professional reports

It's like a "no-code" analytics workspace where non-technical users can make data-driven decisions faster.

---

## Q2: Key Features
**Difficulty:** Easy  
**Question:** Name 5 major features of Datalytics AI.

**Expected Answer (1-2 minutes):**
1. **Dataset Upload** - Support for CSV, Excel, JSON, Google Sheets, APIs, MySQL, PostgreSQL, MongoDB, PDF
2. **Data Exploration (EDA)** - Automatic profiling, column summaries, missing values detection, distributions
3. **Data Preparation** - Cleaning, preprocessing, type conversion, validation
4. **Visualization** - Interactive charts, Plotly dashboards, chart recommendations
5. **Machine Learning** - Model training (supervised & unsupervised), predictions, model comparison
6. **AI Insights** - Groq/OpenAI chatbot, recommendations, decision support
7. **Reports** - PDF/Excel exports with analysis summaries
8. **Admin Panel** - User management, payment tracking, activity logs

---

## Q3: Frontend Technology Stack
**Difficulty:** Easy  
**Question:** What technologies are used for the frontend, and why?

**Expected Answer (1-2 minutes):**
- **Next.js 15** - Modern React framework for server-side rendering, fast page loads
- **React 19** - UI component library for building interactive interfaces
- **Tailwind CSS** - Utility-first CSS for responsive design and quick styling
- **Framer Motion** - Animation library for smooth transitions and visual feedback
- **Three.js** - 3D rendering (for interactive visualizations)
- **Plotly.js** - Interactive charting library
- **Axios** - HTTP client for API calls
- **Firebase** - Authentication and user management

Why: These are industry-standard tools that provide fast, responsive UIs with beautiful animations and real-time updates.

---

## Q4: Backend Technology Stack
**Difficulty:** Easy  
**Question:** What is the backend built with, and what does each component do?

**Expected Answer (1-2 minutes):**
- **FastAPI** - Modern, fast Python web framework for building APIs (10,000 requests/second)
- **Python 3.10+** - Language choice for ML/data science integration
- **Uvicorn** - ASGI server to run FastAPI (faster than WSGI)
- **Motor** - Async MongoDB driver for non-blocking database calls
- **Celery** - Task queue for background jobs (data processing, email sending)
- **Redis** - In-memory cache for fast data retrieval and session storage
- **Pandas/NumPy** - Data manipulation libraries
- **Scikit-learn, XGBoost, CatBoost** - ML model libraries

---

## Q5: Database Choice
**Difficulty:** Easy  
**Question:** Why was MongoDB chosen instead of traditional SQL databases?

**Expected Answer (1-2 minutes):**
MongoDB was chosen because:
1. **Flexible Schema** - Datasets vary in structure; SQL requires predefined schemas
2. **Scalability** - MongoDB scales horizontally (add more servers)
3. **Document-oriented** - Perfect for storing JSON-like data (user profiles, datasets, models)
4. **Speed** - No join operations needed; data is denormalized (fast queries)
5. **Async Support via Motor** - Non-blocking I/O allows handling 10,000+ concurrent users
6. **Real-time queries** - Better for dynamic data analytics

However, SQL is still used for analytics where data relationships are strict.

---

## Q6: Project Architecture Overview
**Difficulty:** Easy  
**Question:** Draw a simple architecture diagram of Datalytics AI.

**Expected Answer (1-2 minutes):**
```
┌─────────────────────────────────┐
│   User Browser (Frontend)       │
│  Next.js Client (port 5000)     │
│  - Upload, Visualize, Train ML  │
└────────────┬────────────────────┘
             │ (HTTPS/WebSocket)
             ▼
┌─────────────────────────────────┐
│  FastAPI Backend (port 8000)    │
│  - Auth, APIs, ML Logic         │
│  - Upload, EDA, Training        │
│  - Reports, Chatbot, Payments   │
└────────────┬────────────────────┘
             │
     ┌───────┴────────┬──────────┬──────────┐
     ▼                ▼          ▼          ▼
┌──────────┐    ┌────────┐  ┌──────┐  ┌──────────┐
│ MongoDB  │    │ Redis  │  │Celery│  │External  │
│(Database)│    │(Cache) │  │(Jobs)│  │APIs      │
└──────────┘    └────────┘  └──────┘  └──────────┘
```

---

## Q7: API Routes & Endpoints
**Difficulty:** Easy  
**Question:** What are the main API route categories in Datalytics?

**Expected Answer (1-2 minutes):**
- `/api/auth` - Login, signup, logout, OTP verification, Google login
- `/api/upload` - File upload, data source connectors
- `/api/data` - Fetch, update, delete datasets
- `/api/eda` - Exploratory data analysis, profiling
- `/api/preprocess` - Data cleaning and transformation
- `/api/train` - ML model training (supervised/unsupervised)
- `/api/predict` - Make predictions on new data
- `/api/visualize` - Create charts and dashboards
- `/api/chatbot` - AI chat for insights
- `/api/reports` - Generate PDF/Excel reports
- `/api/payment` - Handle subscriptions and payments
- `/api/admin` - Admin dashboard and user management
- `/api/activity` - User activity logging

---

## Q8: Authentication Flow
**Difficulty:** Easy  
**Question:** How does user authentication work in Datalytics?

**Expected Answer (1-2 minutes):**
1. **Email/Password Auth**
   - User enters email and password
   - Backend hashes password with bcrypt
   - If valid, JWT token is generated and sent to frontend
   - Frontend stores token in localStorage

2. **OTP Verification**
   - User enters email, gets OTP via email
   - Verifies OTP, gets JWT token

3. **Google OAuth**
   - User clicks "Sign in with Google"
   - Firebase handles OAuth flow
   - Backend verifies and creates JWT token

4. **Token Usage**
   - Every API request includes `Authorization: Bearer <token>`
   - Backend validates token using JWT_SECRET
   - If valid, request proceeds; if invalid, 401 Unauthorized error

---

## Q9: Data Upload Process
**Difficulty:** Easy  
**Question:** Walk through the data upload flow from user perspective.

**Expected Answer (1-2 minutes):**
1. User logs in → UploadStep component opens
2. User selects file (CSV, Excel, JSON) or database connection
3. Frontend sends file/credentials to `/api/upload` endpoint
4. Backend:
   - Validates file format
   - Parses data (pandas.read_csv, openpyxl, etc.)
   - Profiles dataset (column types, missing values, distributions)
   - Stores in MongoDB with session ID
   - Returns preview (first 100 rows)
5. Frontend:
   - Shows data preview
   - Displays basic statistics
   - Marks "upload" as completed
   - Shows "Continue" button to next step

---

## Q10: State Management Frontend
**Difficulty:** Easy  
**Question:** How is state managed in the React frontend?

**Expected Answer (1-2 minutes):**
React uses **local state** with `useState` and **context**:

1. **Local State (useState)**
   - Current step (upload, exploration, prediction)
   - Dataset rows and columns
   - ML model metrics
   - Visualization config

2. **Context (useDataset, useDiamonds)**
   - Global dataset state
   - User credits/diamonds tracking
   - Authentication profile

3. **LocalStorage**
   - Auth token (persists across page reloads)
   - User preferences
   - Completed steps

4. **No Redux** - App is moderately complex, so context + useState is sufficient

The App.jsx file (~1700 lines) manages most state at the root level.

---

## Q11: Machine Learning Models Available
**Difficulty:** Easy  
**Question:** What ML models can users train with Datalytics?

**Expected Answer (1-2 minutes):**
**Supervised Learning:**
- Linear Regression (for numeric predictions)
- Logistic Regression (for classification/yes-no predictions)
- Decision Trees (easy to interpret)
- Random Forest (ensemble, high accuracy)

**Unsupervised Learning:**
- K-Means Clustering (group similar data points)
- PCA (Principal Component Analysis - dimensionality reduction)

**Model Comparison:**
- Displays accuracy, precision, recall, F1-score
- User selects "best" model
- Can make predictions on new data using best model

All models use scikit-learn, XGBoost, or CatBoost libraries.

---

## Q12: Payment & Credit System
**Difficulty:** Easy  
**Question:** How does the payment system work?

**Expected Answer (1-2 minutes):**
Users have **credits/diamonds** that are:
- **Earned**: Free users get 100 credits/month
- **Used**: Each major step costs 20 credits (prediction, power BI, recommendations)
- **Purchased**: Via Razorpay
  - Free Plan: 100 credits/month
  - Basic Plan: 500 credits/month
  - Pro Plan: 2000 credits/month + priority support

When user runs out of credits:
- App shows "Insufficient Credits" alert
- Redirects to pricing page
- User can upgrade plan

Admin tracks all payments in admin panel.

---

## Q13: Admin Panel Features
**Difficulty:** Easy  
**Question:** What can an admin do in the Datalytics admin panel?

**Expected Answer (1-2 minutes):**
- **Analytics Overview** - Total users, active sessions, revenue
- **User Management** - View all users, their credits, activity
- **Payment Tracking** - Subscription plans, invoices, refunds
- **Email Campaigns** - Send announcements, offers, warnings to users
- **Activity Logs** - View user actions (upload, train, visualize)
- **Login/Logout Logs** - Track when users login
- **Edit Admin Profile** - Change admin password, email
- **System Health** - Database status, API uptime

Admin email is hardcoded as `singhsangam5400@gmail.com`.

---

## Q14: Error Handling Strategy
**Difficulty:** Easy  
**Question:** How does the application handle errors?

**Expected Answer (1-2 minutes):**
**Frontend:**
- Try-catch blocks around API calls
- AppErrorBoundary component catches React errors
- Toast notifications show user-friendly messages
- Fallback UI if component crashes

**Backend:**
- FastAPI automatically validates request data (Pydantic)
- Returns HTTP error codes (400 Bad Request, 401 Unauthorized, 500 Server Error)
- Logs errors to console
- Returns JSON error response: `{"detail": "error message"}`

**Example:**
```python
# Backend
if not dataset:
    raise HTTPException(status_code=404, detail="Dataset not found")

# Frontend
try {
    const data = await client.post('/upload', formData)
} catch (error) {
    showToast(error.response?.data?.detail || "Upload failed")
}
```

---

## Q15: Session Management
**Difficulty:** Easy  
**Question:** How does the application track user sessions?

**Expected Answer (1-2 minutes):**
1. **Session ID Middleware** (in main.py)
   - FastAPI middleware generates unique session ID for each request
   - Adds `X-Session-ID` header to response
   - Used to track user activity and prevent CSRF attacks

2. **JWT Token**
   - Stored in localStorage
   - Sent with every request in `Authorization` header
   - Contains user email and role

3. **Activity Logging**
   - Logs are stored in MongoDB with session ID, user email, timestamp
   - Used for admin audit trails
   - Enables activity heatmaps and KPI tracking

---

## Q16: Real-time Updates & WebSocket
**Difficulty:** Easy  
**Question:** Does Datalytics use WebSocket for real-time updates?

**Expected Answer (1-2 minutes):**
Currently **NOT using WebSocket**. The app uses:

1. **Polling** - Frontend periodically asks backend "Is training done?"
2. **Celery Task Status** - For long-running tasks (model training)
   - Backend stores task status in Redis
   - Frontend polls `/api/task/{task_id}/status` every 2 seconds

3. **Potential Improvements:**
   - Could add WebSocket for live training progress
   - Could push notifications when training completes
   - But polling + Redis is sufficient for current load

---

## Q17: CORS Policy
**Difficulty:** Easy  
**Question:** How is CORS (Cross-Origin Resource Sharing) configured?

**Expected Answer (1-2 minutes):**
In `main.py`:
```python
app.add_middleware(
    CORSMiddleware,
    allow_origins=["*"],  # Allow ALL origins
    allow_credentials=True,
    allow_methods=["*"],  # Allow all HTTP methods
    allow_headers=["*"],  # Allow all headers
)
```

**Why:**
- Frontend is at `localhost:5000` or deployed domain
- Backend is at `localhost:8000` or separate domain
- CORS allows cross-origin requests

**Security Note:** `allow_origins=["*"]` is convenient for development but **NOT** for production. Should restrict to specific domains:
```python
allow_origins=["https://datalytics.com", "https://app.datalytics.com"]
```

---

## Q18: File Upload Security
**Difficulty:** Easy  
**Question:** What security measures are used for file uploads?

**Expected Answer (1-2 minutes):**
1. **File Type Validation** - Only CSV, Excel, JSON, PDF allowed
2. **File Size Limit** - Max 100MB per file (prevents disk space abuse)
3. **Content Type Check** - Verify MIME type matches file extension
4. **Virus Scanning** - Optional integration with antivirus API
5. **Sandboxed Processing** - Files processed in temporary directory, then deleted
6. **User Authentication** - Only authenticated users can upload
7. **Rate Limiting** - Limit uploads per user to prevent abuse

---

## Q19: Logging & Monitoring
**Difficulty:** Easy  
**Question:** How does the application log errors and monitor health?

**Expected Answer (1-2 minutes):**
**Logging:**
- `logging` module in Python (INFO, WARNING, ERROR levels)
- All requests logged with timestamp and status code
- Errors written to `.log` files in server directory

**Health Checks:**
- `/health` endpoint returns MongoDB connection status
- Called by load balancer to check if server is alive
- If MongoDB is down, returns 503 Service Unavailable

**Monitoring (Manual for now):**
- Admin can view activity logs in admin panel
- Could integrate with Sentry, DataDog, New Relic for production

---

## Q20: Deployment & Hosting
**Difficulty:** Easy  
**Question:** How is Datalytics deployed to production?

**Expected Answer (1-2 minutes):**
**Current Deployment (Render.com):**
- `render.yaml` file specifies deployment config
- **Frontend (Next.js)**
  - Build command: `npm install && npm run build`
  - Start command: `npm start`
  - Runs on port 5000

- **Backend (FastAPI)**
  - Build command: `pip install -r requirements.txt`
  - Start command: `uvicorn app.main:app --host 0.0.0.0 --port 8000`
  - Runs on port 8000

**Also supports:**
- Docker containers (Dockerfile)
- AWS, Google Cloud, Azure
- Heroku

**Production Considerations:**
- Use environment variables (.env file)
- HTTPS/SSL certificates
- Database backups
- Load balancing
- Auto-scaling

---

# 🟡 MEDIUM QUESTIONS (21-40)

---

## Q21: Session Middleware Implementation
**Difficulty:** Medium  
**Question:** Explain the session middleware in main.py. Why is it needed?

**Expected Answer (1-2 minutes):**
**Code (lines 61-72 in main.py):**
```python
@app.middleware("http")
async def session_middleware(request: Request, call_next):
    session_id = request.headers.get("X-Session-ID")
    if not session_id:
        session_id = str(uuid.uuid4())
        # Add session ID to request headers
    response = await call_next(request)
    response.headers["X-Session-ID"] = session_id
    return response
```

**Why it's needed:**
1. **Request Tracking** - Each request gets unique ID for logging
2. **Activity Audit** - Can link multiple requests to same user session
3. **CSRF Protection** - Prevents cross-site request forgery attacks
4. **Analytics** - Track user behavior across requests
5. **Debugging** - If bug occurs, can find all requests from that session

**Example use case:**
- User uploads 3 files in one session
- Each upload has same session_id
- Admin can see "User X uploaded 3 files in 2 minutes"

---

## Q22: Async/Await Pattern
**Difficulty:** Medium  
**Question:** Why does the backend use async/await? Give an example.

**Expected Answer (1-2 minutes):**
**Async allows non-blocking I/O:**
```python
# ASYNC (Good) - Can handle 1000s of concurrent requests
@app.get("/data/{dataset_id}")
async def get_data(dataset_id: str):
    dataset = await db.datasets.find_one({"_id": dataset_id})
    return dataset

# SYNC (Bad) - Blocks entire thread waiting for DB
@app.get("/data/{dataset_id}")
def get_data(dataset_id: str):
    dataset = db.datasets.find_one({"_id": dataset_id})  # Blocks!
    return dataset
```

**Why it matters:**
- While waiting for DB response, FastAPI can handle OTHER requests
- 1 Uvicorn worker can handle 10,000 concurrent users
- Without async, 10,000 concurrent users = 10,000 blocked threads (impossible)

**Used in FastAPI:**
- Motor (async MongoDB driver)
- Database queries
- External API calls
- File I/O operations

---

## Q23: Celery Task Queue
**Difficulty:** Medium  
**Question:** Why is Celery used, and what kind of tasks does it handle?

**Expected Answer (1-2 minutes):**
**Celery is a task queue** - Runs long-running tasks in background workers.

**Why:**
- User uploads file → Backend returns immediately → Celery processes in background
- Without Celery, user would wait 10 seconds for upload to complete (bad UX)

**Tasks:**
1. **Data Profiling** - Analyze dataset structure, types, missing values
2. **Model Training** - Scikit-learn training can take minutes
3. **Email Sending** - OTP, welcome, notification emails
4. **Report Generation** - PDF/Excel creation
5. **Batch Predictions** - Predict on 1000s of rows

**Architecture:**
```
Frontend → FastAPI → Celery Task Added to Redis Queue
                                        ↓
                            Celery Worker (Background Process)
                            - Picks task from queue
                            - Executes (train model, send email)
                            - Stores result in Redis
                            ↓
Frontend polls: "Is task done?" → Redis → Returns result
```

**In celery_app.py:**
- Broker: Redis (task queue)
- Backend: Redis (stores task results)
- Worker processes tasks one-by-one or in parallel

---

## Q24: API Response Time Optimization
**Difficulty:** Medium  
**Question:** How would you optimize API response time if `/eda` endpoint takes 10 seconds?

**Expected Answer (1-2 minutes):**
**Current Issue:** EDA (Exploratory Data Analysis) takes 10 seconds - too slow!

**Optimization strategies:**
1. **Caching** - Cache EDA results in Redis for 1 hour
   ```python
   @app.get("/eda/{dataset_id}")
   async def eda(dataset_id: str):
       cached = await redis.get(f"eda:{dataset_id}")
       if cached: return cached  # Return in 10ms
       
       result = compute_eda(dataset)
       await redis.set(f"eda:{dataset_id}", result, ex=3600)  # Cache for 1hr
       return result
   ```

2. **Database Indexing** - Index frequently queried fields
3. **Pagination** - Return only first 100 rows instead of all
4. **Async Processing** - Use Celery for heavy computation
5. **Database Sharding** - Split data across multiple databases
6. **Query Optimization** - Use aggregation pipeline in MongoDB
7. **CDN** - Cache static visualizations
8. **Load Balancing** - Distribute requests across servers

**Expected result:** 10 seconds → 100ms (100x faster!)

---

## Q25: Database Connection Pooling
**Difficulty:** Medium  
**Question:** What is connection pooling, and why is it important?

**Expected Answer (1-2 minutes):**
**Connection pooling = reusing database connections instead of creating new ones.**

**Without pooling:**
```
Request 1 → Create connection → Query → Close connection (slow, 100ms)
Request 2 → Create connection → Query → Close connection (slow, 100ms)
```

**With pooling:**
```
Pre-created 10 connections in pool
Request 1 → Borrow from pool (1ms) → Query → Return to pool
Request 2 → Borrow from pool (1ms) → Query → Return to pool
```

**Benefits:**
- 100x faster connection time
- Reduced CPU/memory usage
- Can handle more concurrent requests

**In Datalytics:**
- Motor (async MongoDB driver) handles connection pooling automatically
- Max 50 connections by default (configurable)

**Code:**
```python
from motor.motor_asyncio import AsyncClient
client = AsyncClient('mongodb://...', max_pool_size=50)
db = client.datalytics
```

---

## Q26: Data Validation
**Difficulty:** Medium  
**Question:** How does FastAPI validate user input?

**Expected Answer (1-2 minutes):**
**FastAPI uses Pydantic models for validation:**

```python
from pydantic import BaseModel, EmailStr, Field

class UserSignup(BaseModel):
    email: EmailStr  # Must be valid email
    password: str = Field(..., min_length=8)  # Min 8 chars
    name: str = Field(..., min_length=1)  # Required

@app.post("/signup")
async def signup(user: UserSignup):
    # If email not valid → 422 Unprocessable Entity
    # If password < 8 chars → 422
    # If name empty → 422
    return {"message": "Signup successful"}
```

**Validations:**
- **Type checking** - email must be string, age must be int
- **Email validation** - Must be valid email format
- **Length validation** - Min/max string length
- **Numeric validation** - Min/max values
- **Pattern validation** - Regex matching
- **Custom validation** - User-defined rules

**Benefits:**
- Invalid data rejected before reaching database
- Automatic error messages returned to frontend
- Prevents SQL injection, malformed data

---

## Q27: Error Handling & Status Codes
**Difficulty:** Medium  
**Question:** What HTTP status codes should API return, and when?

**Expected Answer (1-2 minutes):**
**2xx Success:**
- 200 OK - Request succeeded, data returned
- 201 Created - New resource created (POST request)
- 204 No Content - Success, no data to return

**4xx Client Error (client's fault):**
- 400 Bad Request - Invalid input (missing fields, wrong type)
- 401 Unauthorized - No auth token provided
- 403 Forbidden - Auth token valid but user not allowed
- 404 Not Found - Resource doesn't exist
- 422 Unprocessable Entity - Data validation failed

**5xx Server Error (server's fault):**
- 500 Internal Server Error - Unexpected error
- 502 Bad Gateway - Backend unreachable
- 503 Service Unavailable - Server overloaded or maintenance

**Example:**
```python
@app.post("/train-model")
async def train_model(dataset_id: str):
    if not dataset_id:
        raise HTTPException(status_code=400, detail="dataset_id required")
    
    dataset = await db.datasets.find_one({"_id": dataset_id})
    if not dataset:
        raise HTTPException(status_code=404, detail="Dataset not found")
    
    # ... train model ...
    return {"status": 200, "message": "Model trained"}
```

---

## Q28: Rate Limiting
**Difficulty:** Medium  
**Question:** How would you implement rate limiting to prevent API abuse?

**Expected Answer (1-2 minutes):**
**Rate limiting = limit requests per user to prevent abuse.**

**Without rate limiting:**
- Attacker sends 10,000 requests/second
- Server overloads, becomes slow for everyone

**With rate limiting:**
- User can send max 100 requests/minute
- After 100, returns 429 Too Many Requests
- Resets every minute

**Implementation using Redis:**
```python
from slowapi import Limiter
from slowapi.util import get_remote_address

limiter = Limiter(key_func=get_remote_address)

@app.post("/upload")
@limiter.limit("5/minute")  # Max 5 uploads per minute per IP
async def upload_file(file: UploadFile):
    return {"message": "File uploaded"}
```

**Per-user rate limiting:**
- Free users: 100 requests/day
- Premium users: 10,000 requests/day
- Track in Redis: `rate_limit:{user_id}:{date}` = current_count

**Benefits:**
- Prevents DDoS attacks
- Prevents accidental API abuse
- Fair usage among users

---

## Q29: Database Transactions
**Difficulty:** Medium  
**Question:** How would you ensure payment goes through ONLY if credits are successfully deducted?

**Expected Answer (1-2 minutes):**
**Use database transactions to ensure atomicity (all-or-nothing):**

```python
# Without transactions (WRONG):
# If server crashes between steps 3-4, user loses credits but payment goes through

from motor.motor_asyncio import AsyncSession

async def purchase_credits(user_id, amount):
    # Step 1: Charge payment via Razorpay
    payment = await razorpay.charge(user_id, amount)
    
    # Step 2: Deduct credits from user
    # PROBLEM: If server crashes here, payment taken but credits not added
    await db.users.update_one(
        {"_id": user_id},
        {"$inc": {"credits": amount}}
    )
    
    # With transactions (CORRECT):
    async with await client.start_session() as session:
        async with session.start_transaction():
            # Both operations succeed or both fail
            await razorpay.charge(user_id, amount)
            await db.users.update_one(
                {"_id": user_id},
                {"$inc": {"credits": amount}}
            )
            # If either fails, transaction rolls back
```

**Benefits:**
- No data inconsistency
- Prevents money loss
- Protects user trust

---

## Q30: Caching Strategy
**Difficulty:** Medium  
**Question:** What data should be cached in Redis, and for how long?

**Expected Answer (1-2 minutes):**
**Cache expensive operations, not frequently-changing data:**

| Data | Cache Duration | Why |
|------|---|---|
| EDA results | 1 hour | Computing stats on 1M rows takes 10s |
| User profile | 5 mins | Changes infrequently |
| ML model | 1 hour | Training takes 5 minutes |
| Dataset preview | 30 mins | User won't change data often |
| API responses | 5-60 mins | Depends on data freshness |
| Auth tokens | 24 hours | Prevent re-login on page refresh |
| **DO NOT cache:** | | |
| Predictions | - | Always fresh based on current data |
| Real-time analytics | - | Must be current |
| Admin logs | - | Must be accurate audit trail |

**Implementation:**
```python
async def get_eda_results(dataset_id: str):
    cache_key = f"eda:{dataset_id}"
    
    # Try cache first
    cached = await redis.get(cache_key)
    if cached:
        return json.loads(cached)
    
    # If not cached, compute
    result = await compute_eda(dataset_id)
    
    # Cache for 1 hour
    await redis.setex(cache_key, 3600, json.dumps(result))
    
    return result
```

---

## Q31: Scaling to 10,000 Concurrent Users
**Difficulty:** Medium  
**Question:** How would you scale Datalytics to handle 10,000 concurrent users?

**Expected Answer (1-2 minutes):**
**Current setup can handle ~1,000 concurrent users. To reach 10,000:**

1. **Load Balancing** - Use Nginx or load balancer
   - Distribute traffic across 10 backend servers
   - Each server handles 1,000 users

2. **Horizontal Scaling**
   - Run 10 instances of FastAPI backend
   - Each with 50 Uvicorn workers
   - Total: 500 workers handling 10,000 concurrent requests

3. **Database Optimization**
   - MongoDB sharding (split data across 5 databases)
   - Increase connection pool to 100
   - Add read replicas for reports

4. **Caching**
   - Redis cluster (3 nodes) instead of single instance
   - Cache EDA, model results, user profiles
   - Reduces database load by 80%

5. **Celery Workers**
   - 20 Celery workers for background tasks
   - Handle model training, email, reports in parallel

6. **CDN** - Serve static assets (images, CSS) from CDN

7. **Database Indexing** - Index frequently queried fields

**Architecture:**
```
10,000 users
    ↓
Nginx Load Balancer
    ↓
10 FastAPI Servers
    ↓
MongoDB Cluster (sharded) + Redis Cluster
```

---

## Q32: Frontend Performance Optimization
**Difficulty:** Medium  
**Question:** How is the Next.js frontend optimized for performance?

**Expected Answer (1-2 minutes):**
**Optimizations in place:**

1. **Code Splitting** - Components loaded on-demand
   ```jsx
   const ExploreStep = lazy(() => import('./ExploreStep.jsx'))
   ```

2. **Image Optimization** - Automatic WebP conversion
3. **CSS-in-JS** - Tailwind generates only needed CSS
4. **Caching Headers** - Static assets cached 1 year
5. **Compression** - Gzip compression for JS/CSS
6. **Service Workers** - PWA for offline support

**Performance improvements:**
- First paint: 2 seconds (from 5 seconds)
- Time to interactive: 3 seconds (from 8 seconds)

---

## Q33: Data Pipeline Workflow
**Difficulty:** Medium  
**Question:** Trace the complete flow from file upload to model prediction.

**Expected Answer (1-2 minutes):**
1. **Upload** → User selects CSV file
2. **Parsing** → Backend reads CSV using Pandas
3. **Profiling** → EDA computes stats (5 seconds)
4. **Cleaning** → User removes duplicates, handles missing values
5. **Exploration** → Display distributions, correlations
6. **Visualization** → Create charts (Plotly)
7. **Preprocessing** → Normalize data, split train/test (80/20)
8. **Training** → Scikit-learn trains 4 models (2 minutes)
9. **Comparison** → Display metrics, user picks best model
10. **Prediction** → User enters new data, model predicts
11. **Report** → PDF export with charts and insights

**Stored in:**
- MongoDB: Dataset, model metadata, predictions
- Redis: Session state, cached results
- File system: Temporary uploads, trained models

---

## Q34: Error Recovery
**Difficulty:** Medium  
**Question:** What happens if model training fails halfway through?

**Expected Answer (1-2 minutes):**
**Scenario:** Training 10,000 rows, fails at 50%.

**Recovery:**
1. **Celery detects failure** - Task threw exception
2. **Error logged** - Stored in Celery backend (Redis)
3. **User notified** - "Model training failed. Retrying..."
4. **Retry logic** - Automatically retry up to 3 times
5. **If still fails** - Show error message to user

**Code:**
```python
@app.post("/train")
async def train_model(dataset_id: str):
    try:
        task = train_model_task.apply_async(
            args=[dataset_id],
            retry=True,
            retry_policy={
                'max_retries': 3,
                'interval_start': 1,
                'interval_step': 0.2,
                'interval_max': 0.2,
            }
        )
        return {"task_id": task.id}
    except Exception as e:
        log.error(f"Training failed: {e}")
        return {"error": "Training failed. Please try again."}
```

---

## Q35: Security Best Practices
**Difficulty:** Medium  
**Question:** What security measures protect user data?

**Expected Answer (1-2 minutes):**
1. **Password Hashing** - BCrypt hashes passwords (not stored plaintext)
2. **JWT Tokens** - Stateless authentication, can't be forged
3. **HTTPS/SSL** - Encrypts data in transit
4. **Input Validation** - Pydantic rejects invalid data
5. **SQL Injection Prevention** - Using ORM (Motor), not raw queries
6. **CORS Policy** - Restricts cross-origin requests
7. **Rate Limiting** - Prevents brute-force attacks
8. **Environment Variables** - API keys not in code
9. **Auth Token Expiry** - Token expires after 24 hours
10. **Activity Logging** - Track suspicious access patterns

---

## Q36: Monitoring & Observability
**Difficulty:** Medium  
**Question:** How would you monitor Datalytics in production?

**Expected Answer (1-2 minutes):**
**Key metrics to track:**

1. **Application Metrics**
   - API response times
   - Request error rates
   - Model training duration

2. **Infrastructure Metrics**
   - CPU/memory usage
   - Database query times
   - Redis memory usage

3. **Business Metrics**
   - Active users
   - Models trained per day
   - Revenue from subscriptions

**Tools:**
- **Prometheus** - Collect metrics
- **Grafana** - Visualize metrics
- **Sentry** - Error tracking
- **DataDog** - Real-time monitoring
- **New Relic** - APM (application performance monitoring)

**Alerts:**
- If error rate > 1%, alert on-call engineer
- If response time > 5s, investigate
- If database down, auto-failover to replica

---

## Q37: Testing Strategy
**Difficulty:** Medium  
**Question:** What tests should be written for the API?

**Expected Answer (1-2 minutes):**
**Unit Tests:**
```python
def test_password_validation():
    assert validate_password("abc") == False  # Too short
    assert validate_password("Valid123!") == True

def test_email_validation():
    assert validate_email("user@gmail.com") == True
    assert validate_email("invalid") == False
```

**Integration Tests:**
```python
async def test_signup_flow():
    response = await client.post("/signup", json={
        "email": "user@gmail.com",
        "password": "ValidPass123"
    })
    assert response.status_code == 201
    assert response.json()["token"]  # JWT token returned
```

**API Tests:**
```python
async def test_upload_csv():
    with open("test.csv") as file:
        response = await client.post("/upload", files={"file": file})
    assert response.status_code == 200
    assert "dataset_id" in response.json()
```

**E2E Tests:**
```python
async def test_complete_workflow():
    # 1. Sign up
    user = await signup("user@test.com", "pass123")
    # 2. Upload file
    dataset = await upload_file(user, "test.csv")
    # 3. Train model
    model = await train_model(user, dataset)
    # 4. Make prediction
    prediction = await predict(user, model, {"age": 25})
    assert prediction["result"] > 0
```

---

## Q38: Deployment Checklist
**Difficulty:** Medium  
**Question:** What should be verified before deploying to production?

**Expected Answer (1-2 minutes):**
✅ **Code Quality**
- No hardcoded secrets (use .env)
- Error handling on all API endpoints
- Input validation on all endpoints
- All tests passing

✅ **Security**
- HTTPS/SSL enabled
- JWT tokens working
- CORS properly configured
- Rate limiting enabled

✅ **Performance**
- API response time < 500ms
- Database queries optimized
- Caching enabled
- Load testing passed

✅ **Operations**
- Error monitoring (Sentry)
- Performance monitoring (DataDog)
- Database backups configured
- Log aggregation (ELK stack)
- Disaster recovery plan

✅ **Documentation**
- API docs up-to-date
- Deployment guide written
- Runbook for common issues

---

## Q39: Backward Compatibility
**Difficulty:** Medium  
**Question:** How do you deploy new API changes without breaking existing clients?

**Expected Answer (1-2 minutes):**
**Scenario:** Old mobile app expects `/api/v1/train`, new app expects `/api/v2/train`

**Solutions:**

1. **API Versioning**
   ```python
   @app.post("/api/v1/train")  # Old endpoint
   async def train_v1(): ...
   
   @app.post("/api/v2/train")  # New endpoint
   async def train_v2(): ...
   ```

2. **Feature Flags**
   ```python
   if user.plan == "premium":
       return new_feature_response()
   else:
       return old_feature_response()
   ```

3. **Gradual Rollout**
   - Deploy to 10% of users, monitor errors
   - If good, deploy to 50%, then 100%

4. **Deprecation Period**
   - Announce v1 endpoint deprecated
   - Give users 6 months to upgrade
   - Then remove v1

---

## Q40: Multi-tenant Architecture
**Difficulty:** Medium  
**Question:** Can Datalytics support multiple organizations (SaaS)?

**Expected Answer (1-2 minutes):**
**Current:** Single-tenant (all users share same data)  
**To make multi-tenant:**

1. **Add org_id to all collections**
   ```python
   {
       "_id": "dataset_123",
       "org_id": "org_abc",  # Which organization owns this
       "name": "Sales Data",
       "data": [...]
   }
   ```

2. **Middleware isolation**
   ```python
   @app.middleware("http")
   async def org_isolation(request, call_next):
       token = request.headers.get("Authorization")
       user = decode_jwt(token)
       request.state.org_id = user.org_id
       response = await call_next(request)
       return response
   ```

3. **Queries filter by org_id**
   ```python
   datasets = await db.datasets.find({
       "org_id": request.state.org_id  # Only this org's data
   })
   ```

4. **Storage isolation**
   - Separate MongoDB databases per org
   - Or separate shards

5. **Billing per org**
   - Track credits per organization
   - Separate payment plans

---

# 🔴 HARD QUESTIONS (41-50)

---

## Q41: Designing High-Availability System
**Difficulty:** Hard  
**Question:** Design a highly-available Datalytics that survives single-server failure.

**Expected Answer (1-2 minutes):**
**Current weakness:** Single point of failure if main server goes down.

**High-Availability Design:**
```
Users (Load Balancer)
    ↓
[Server 1] [Server 2] [Server 3]  (Any 1 can fail)
    ↓
MongoDB Replica Set (Primary + 2 secondaries)
    - If Primary fails, election happens
    - Secondary becomes Primary automatically
    ↓
Redis Cluster (3 nodes)
    - If 1 node fails, cluster still works
```

**Redundancy:**
- 3+ FastAPI servers (active-active)
- MongoDB replication (auto-failover)
- Redis cluster (no single point of failure)
- Database backups (hourly)

**Auto-recovery:**
- Health checks every 10 seconds
- If Server 1 unhealthy, remove from load balancer
- Auto-restart failed services (Kubernetes)

**Result:** 99.99% uptime (4 nines)

---

## Q42: Distributed System Consistency
**Difficulty:** Hard  
**Question:** How do you ensure consistency when users modify same dataset simultaneously?

**Expected Answer (1-2 minutes):**
**Scenario:** 
- User A removes row 5
- User B adds column at same time
- Result: Data corruption?

**Solutions:**

1. **Pessimistic Locking** (Lock entire dataset)
   ```python
   # User A locks dataset
   await db.datasets.update_one(
       {"_id": dataset_id},
       {"$set": {"locked": True}}
   )
   # User B gets error: "Dataset is being edited"
   ```
   Problem: If User A crashes, dataset locked forever

2. **Optimistic Locking** (Use version numbers)
   ```python
   # User A reads dataset (version=5)
   # User B reads dataset (version=5)
   # User A saves changes → version=6
   # User B tries save → version still 5 → Conflict!
   # User B must re-read and merge changes
   ```

3. **Event Sourcing** (Log all changes)
   ```python
   events = [
       {"type": "RemoveRow", "row_id": 5, "timestamp": 1000},
       {"type": "AddColumn", "name": "Age", "timestamp": 1005},
   ]
   # Replay events in order → consistent final state
   ```

**Datalytics choice:** Pessimistic locking (dataset locked while user editing)

---

## Q43: ML Model Versioning
**Difficulty:** Hard  
**Question:** How do you manage multiple versions of ML models?

**Expected Answer (1-2 minutes):**
**Scenario:** You train 10 models for same dataset over time. Which one is in production?

**Solution:**

```python
# Store model metadata in MongoDB
{
    "_id": ObjectId(),
    "dataset_id": "dataset_123",
    "created_at": "2024-01-15",
    "version": 3,
    "type": "RandomForest",
    "accuracy": 0.95,
    "model_path": "s3://bucket/models/rf_v3.pkl",
    "status": "production",  # or "staging", "archived"
    "trained_by": "user_abc",
}
```

**Versioning strategy:**
- Auto-increment version number
- Tag as "production" or "staging"
- Keep last 5 versions for rollback
- Archive old versions after 1 year

**Deployment:**
```python
@app.post("/predict")
async def predict(dataset_id: str, data: dict):
    model = await db.models.find_one({
        "dataset_id": dataset_id,
        "status": "production"
    })
    prediction = model.predict(data)
    return prediction
```

**Rollback if new model bad:**
```python
# Switch back to v2
await db.models.update_one(
    {"dataset_id": "dataset_123", "version": 2},
    {"$set": {"status": "production"}}
)
```

---

## Q44: Handling Data Pipeline Failures
**Difficulty:** Hard  
**Question:** If model training fails after 30 minutes of computation, how do you recover?

**Expected Answer (1-2 minutes):**
**Problem:** User waits 30 minutes, then training fails. They're angry!

**Solutions:**

1. **Checkpointing** - Save progress every 5 minutes
   ```python
   # Training Loop
   for epoch in range(100):
       train_model()
       if epoch % 5 == 0:
           save_checkpoint(f"model_epoch_{epoch}.pkl")
   
   # If fails at epoch 87:
   # Restart from epoch 85 checkpoint (10 min loss, not 30)
   ```

2. **Partial Results**
   ```python
   return {
       "completed_epochs": 87,
       "accuracy_so_far": 0.89,
       "message": "Training interrupted. Can resume later?"
   }
   ```

3. **Async Monitoring**
   ```python
   # Celery task with progress callback
   @celery_app.task(bind=True)
   def train_model_task(self, dataset_id):
       for epoch in range(100):
           self.update_state(state='PROGRESS', meta={'epoch': epoch})
           # Frontend polls and shows "Epoch 45/100"
   ```

4. **Dead Letter Queue**
   ```
   Failed tasks → DLQ → Alert engineer → Manual investigation
   ```

**Result:** 30 min training failure → Resume from checkpoint (5 min loss)

---

## Q45: Handling Sudden Traffic Spikes
**Difficulty:** Hard  
**Question:** If users spike from 100 to 10,000 in 1 minute, what happens?

**Expected Answer (1-2 minutes):**
**Scenario:** Datalytics goes viral on Twitter. Traffic 100x.

**Auto-Scaling Response:**

1. **Kubernetes auto-scaling**
   ```yaml
   apiVersion: autoscaling/v2
   kind: HorizontalPodAutoscaler
   metadata:
     name: api-autoscaler
   spec:
     scaleTargetRef:
       kind: Deployment
       name: api-server
     minReplicas: 2
     maxReplicas: 50
     targetCPUUtilizationPercentage: 70
   ```
   - If CPU > 70%, add 5 more servers
   - Scales to 50 servers in 5 minutes

2. **Load Balancer**
   - Distributes traffic across servers
   - Doesn't overload any single server

3. **Database Read Replicas**
   - Queries distributed across 5 read replicas
   - Write still goes to primary

4. **Caching** (Redis)
   - 80% of requests hit cache (not database)
   - Cache hit rate: 100ms, cache miss: 500ms

5. **Request Queuing**
   - If 10,000 simultaneous requests, 1000 queued
   - Handled as servers free up

6. **Rate Limiting**
   - Free users: 10 req/sec limit
   - Premium users: 100 req/sec limit
   - Prevents single user from hogging resources

**Timeline:**
- 0s: Traffic spike detected
- 30s: Kubernetes starts 10 new servers
- 2min: 20 new servers online
- 5min: 50 servers online, handling 10,000 users
- 15min: Traffic normalizes, servers scale down

---

## Q46: Real-time Notifications Architecture
**Difficulty:** Hard  
**Question:** Design a real-time notification system (model training complete, payment received).

**Expected Answer (1-2 minutes):**
**Current:** Frontend polls every 5 seconds (wasteful)  
**Better:** WebSocket push notifications

**Architecture:**
```
Celery Task (Model Training)
    ↓
    Task Complete → Emit Event
    ↓
Event Stream (Kafka/Redis Pub-Sub)
    ↓
Notification Service (Node.js / Python)
    ↓
WebSocket Server
    ↓
[User 1] [User 2] [User 3] ← Connected
    ↑
Get real-time update: "Training complete!"
```

**Implementation:**

1. **Backend detects event**
   ```python
   @celery_app.task
   def train_model_task(dataset_id, user_id):
       # Train model...
       # Emit event
       await redis.publish(
           f"user:{user_id}:notifications",
           json.dumps({"type": "model_complete", "dataset_id": dataset_id})
       )
   ```

2. **WebSocket server listens**
   ```javascript
   // Socket.io server
   io.on("connection", (socket) => {
       const userId = socket.userId;
       // Subscribe to user's notification channel
       redis.subscribe(`user:${userId}:notifications`);
   });
   ```

3. **Frontend receives**
   ```javascript
   socket.on("model_complete", (data) => {
       toast.success("Model training finished!");
       // Update UI
   });
   ```

**Benefits:**
- 0.1s latency (vs 5s polling)
- Lower bandwidth (push only when needed)
- Better UX

---

## Q47: Data Privacy & GDPR Compliance
**Difficulty:** Hard  
**Question:** How do you handle "right to be forgotten" (GDPR)?

**Expected Answer (1-2 minutes):**
**Requirement:** User can request account deletion. All their data must be removed in 30 days.

**Implementation:**

1. **Mark for Deletion**
   ```python
   @app.post("/user/delete")
   async def delete_user(user_id: str):
       await db.users.update_one(
           {"_id": user_id},
           {"$set": {"deletion_requested_at": datetime.now()}}
       )
       send_confirmation_email(user_id)
       return {"message": "Deletion request received. Confirm email."}
   ```

2. **Cascade Delete** (After confirmation or 30 days)
   ```python
   async def purge_deleted_users():
       cutoff_date = datetime.now() - timedelta(days=30)
       deleted_users = await db.users.find({
           "deletion_requested_at": {"$lt": cutoff_date}
       })
       
       for user in deleted_users:
           # Delete all data
           await db.datasets.delete_many({"user_id": user["_id"]})
           await db.models.delete_many({"user_id": user["_id"]})
           await db.activity_logs.delete_many({"user_id": user["_id"]})
           await db.users.delete_one({"_id": user["_id"]})
   ```

3. **Backups** - Can't fully delete from backups
   - Encrypt backups with user's encryption key
   - Delete key when user deleted (makes backup unreadable)

4. **Audit Trail**
   - Keep deletion log (for compliance)
   - Don't store actual data, just "User 123 deleted on 2024-01-20"

---

## Q48: Cost Optimization
**Difficulty:** Hard  
**Question:** Datalytics costs $100K/month. How would you reduce to $50K?

**Expected Answer (1-2 minutes):**
**Cost Breakdown:**
- Infrastructure: $40K (servers, databases)
- Data Transfer: $30K (bandwidth)
- Third-party APIs: $20K (Groq, OpenAI, Razorpay)
- Team: $10K (salaries allocated)

**Optimizations:**

1. **Infrastructure (-$20K)**
   - Switch to reserved instances (30% discount)
   - Use smaller servers, auto-scale to demand
   - Compress data (reduces storage by 40%)

2. **Data Transfer (-$10K)**
   - Use CDN (CloudFront) for static assets
   - Compress API responses with gzip
   - Batch requests (fewer API calls)

3. **APIs (-$10K)**
   - Switch from OpenAI (expensive) to Groq (cheaper)
   - Cache API responses
   - Implement in-house models instead of calling APIs

4. **Database (-$5K)**
   - Use cheaper storage tiers
   - Archive old datasets to cold storage
   - Implement data retention policy (delete > 1 year old)

5. **Code Optimization (-$5K)**
   - Optimize queries (reduce DB load)
   - Cache heavily (fewer computations)
   - Batch processes (fewer parallel jobs)

**Result:** $100K → $50K/month (50% savings)

---

## Q49: Disaster Recovery Plan
**Difficulty:** Hard  
**Question:** MongoDB is down. How do you recover in 1 hour?

**Expected Answer (1-2 minutes):**
**RTO (Recovery Time Objective): 1 hour**  
**RPO (Recovery Point Objective): 30 mins (max data loss)**

**Disaster Recovery Steps:**

1. **Detect Failure** (1 min)
   ```python
   # Health check fails
   response = await mongodb_cluster.ping()
   if not response:
       trigger_incident()  # Alert on-call engineer
   ```

2. **Failover to Replica** (5 min)
   ```
   Primary MongoDB Down
        ↓
   Secondary MongoDB elected as Primary (auto)
   Application continues with new Primary
   ```

3. **Restore from Backup** (30 min)
   - Hourly backups stored in S3
   - Spin up new MongoDB cluster
   - Restore latest backup
   - Run consistency check

4. **Switch Traffic** (5 min)
   ```
   Old cluster (failed) → New cluster (restored)
   Update connection string
   Verify data integrity
   ```

**Total Recovery: 45 minutes** ✓ (under 1 hour SLA)

**Prevention:**
- Database replication (3 nodes)
- Automatic backups every hour
- Test restore procedure quarterly
- Monitor database health continuously

---

## Q50: Scaling to 1 Million Users
**Difficulty:** Hard  
**Question:** Design Datalytics to support 1 million concurrent users.

**Expected Answer (1-2 minutes):**
**Current capacity:** 10,000 users  
**Target:** 1,000,000 users (100x growth)

**Architecture:**
```
1M Users (Global)
    ↓
CDN (CloudFront) - Serve static content from edge
    ↓
Geographic Load Balancing
    ├─ US: 3 regions
    ├─ EU: 2 regions
    ├─ Asia: 2 regions
    ↓
Regional API Clusters (7 regions)
    Each cluster: 100 FastAPI servers
    Total: 700 servers
    ↓
Database Layer
    ├─ MongoDB Sharded (7 shards, 1 per region)
    ├─ Redis Cluster (distributed across regions)
    └─ Search: Elasticsearch (for full-text search)
```

**Sharding Strategy:**
```python
# Shard by user_id (hash)
shard_id = hash(user_id) % 7

# Route user to their shard
db = connections[shard_id]
await db.users.find_one({"_id": user_id})
```

**Performance:**
- API response: 100ms (90th percentile)
- Model training: Distributed across 100s machines
- Data transfer: CDN (50ms first byte)

**Costs:** ~$1M/month (at scale)

**Challenges:**
- Distributed tracing (where does request go?)
- Consistency across shards (distributed transactions)
- Debugging (logs from 700 servers)
- Data residency (GDPR - keep EU data in EU)

---

## BONUS: Interview Tips

### Tips for Answering Hard Questions:
1. **Start with the problem** - State what you're optimizing for (latency, cost, reliability)
2. **Diagram it** - Draw architecture on whiteboard
3. **Mention trade-offs** - "We could use X, but Y is better because..."
4. **Think operational** - How do you monitor, debug, and recover?
5. **Ask clarifying questions** - "Do we need 99.99% uptime or 99.9%?"

### Most Likely Questions in Interviews:
- **Q1, Q2, Q3** - About the project (everyone asks)
- **Q24, Q25** - Performance optimization
- **Q31** - Scaling (very common)
- **Q45** - Traffic spikes
- **Q50** - Million users (bonus impressive answer)

### How to Prepare:
1. **Understand the code** - Read main.py, App.jsx completely
2. **Study the architecture** - Draw it 10 times
3. **Know the tech stack** - Why FastAPI, MongoDB, Next.js?
4. **Think at scale** - 1M users, 10,000 concurrent users
5. **Know failure scenarios** - "What if X goes down?"

---

## Summary Table: Question Difficulty Distribution

| Category | Count | Focus Areas |
|----------|-------|------------|
| **Easy (Q1-Q20)** | 20 | Overview, features, stack, basics |
| **Medium (Q21-Q40)** | 20 | Architecture, APIs, optimization, security |
| **Hard (Q41-Q50)** | 10 | System design, scale, resilience, disasters |
| **TOTAL** | **50** | Full-stack end-to-end coverage |

---

**Good luck with your interviews! 🚀**

*Remember: Interviewers want to see how you think, not just if you know the answer.*
