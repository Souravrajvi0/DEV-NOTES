Harkirat continues our journey in building a comprehensive Exchange Platform this week, expanding on the foundation we laid in our previous session.

  

Recap: Frontend and Exchange Basics

1] HTTP Endpoints

2] Websocket Streaming

3] Unique Aspects

4] Backend Architecture

5] Pub/Sub System

Key Takeaways

  

> While there are `no specific notes` provided for this section, a mini guide is outlined below to assist you in navigating through the process of building the application. Therefore, it is strongly `advised to actively follow along` during the lecture for a hands-on learning experience.

  

### Recap: Frontend and Exchange Basics

1. **Exchange Terminology**
    - Base asset
    - Quote asset
    - Orderbooks
    - Liquidity
    - Limit orders
    - Market orders
    - KLines (Candlestick charts)
2. **Frontend Development**
    - Implemented proxy requests (e.g., [https://exchange-proxy.100xdevs.com/api/v1/depth?symbol=SHFL_USDC](https://exchange-proxy.100xdevs.com/api/v1/depth?symbol=SHFL_USDC))
    - Created basic frontend components: depth chart, orderbook, ticker
    - Assignment: Develop a 'trades' tab

  

### **1] HTTP Endpoints**

- Get klines: Historical price data
- Get depth: Order book data
- Get Tickers: Current market information

### **2] Websocket Streaming**

- Supported streams: trades, depth, ticker

### **3] Unique Aspects**

- Orderbook maintained in memory
- User balances stored in memory
- Balance locking mechanism in memory

  

### **4] Backend Architecture**

![Untitled 2.png](../../../Images/Untitled%202.png)

The backend architecture image shows a complex system with multiple components:

- Browser: Sends POST requests to the API
- API: Handles incoming requests
- Engine: Processes orders, manages balances
- Websocket: Provides real-time updates
- DB Processor: Persists data to the database
- Redis: Used for queues and pub/sub messaging
- Time series DB: Stores historical price data
- Database processor: Handles data storage operations

Key flows:

- API receives orders and communicates with the Engine
- Engine processes orders and publishes updates
- Websocket provides real-time data to the browser
- Redis facilitates communication between components
- DB Processor ensures data persistence

  

### **5] Pub/Sub System**

  
The pub/sub image illustrates:  

![Untitled 1 2.png](../../../Images/Untitled%201%202.png)

- NodeJS process publishing a ticker update (GOOGLE_USD - 200.2)
- Pub/sub system distributing this update to multiple subscribers:
    - Golang process
    - Rust process

This demonstrates how a single update can be efficiently broadcast to multiple interested parties, enabling real-time data flow across different parts of the system.

1. **Singletons**
    - Purpose: Maintain a single instance of a class throughout the program
    - Reference: [https://www.freecodecamp.org/news/singleton-design-pattern-with-javascript/](https://www.freecodecamp.org/news/singleton-design-pattern-with-javascript/)

### Key Takeaways

1. Backend development builds upon frontend knowledge
2. Complex architecture involves multiple specialized components
3. In-memory operations for performance-critical tasks
4. Pub/sub systems enable efficient real-time updates
5. Design patterns like Singletons play crucial roles in system architecture