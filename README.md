# Michael Yang

I'm a computer science and data science student at UW–Madison, graduating in May 2027. Most of what I build is trading infrastructure and backend systems: an exchange and matching engine in C++, an automated trading system that I run with my own money, and, last summer, product features for BlackRock's advisor-facing AI platform.

Before college I competed in USACO and reached the Platinum division, writing C++.

Email: michaelslyang@gmail.com
LinkedIn: [michael-yang-78173726b](https://www.linkedin.com/in/michael-yang-78173726b)

## Experience

**BlackRock, Aladdin (ChatBLK AI team).** Software engineering intern, June to August 2026, New York.

I built and deployed three full-stack features on ChatBLK, BlackRock's conversational AI platform for financial advisors. The work ran across async Python services, gRPC/protobuf APIs, SQL pipelines on Snowflake, and React 18 front ends.

- The backend for a portfolio-analysis agent: an async httpx client and tool handlers that map portfolio-analysis APIs to LLM function-calling schemas, plus modules for tax transitions, iBonds ladders, and RAG-based market insights.
- A recommender that matches an advisor's client preferences to the best fit among 208 model portfolios. The scoring engine is deterministic Python and returns results almost instantly. The front end is a React/TypeScript quiz with weight sliders and hard filters, tested with Vitest.
- A working voice agent that walks advisors through model portfolios, recommends a best fit, and writes custom rebalance commentary.

**SoftCom Lab, Cal Poly Pomona.** Research intern, March 2023 to August 2024.

This was during high school. I built GolfBud1, a golf-swing analysis app with a Flask API on AWS EC2, a Flutter front end, and Firebase storage. It reached over 5,000 downloads. We filed a provisional patent, and I co-authored a paper that I presented at CMCA 2023. On the ML side, I improved MediaPipe pose-estimation accuracy for swing analysis by 15% using SVMs and decision trees, tuned keypoint thresholds, and multi-angle detection.

**Coding Mind Academy.** Program developer, since August 2023.

I wrote REST backend services in Java, Spring Boot, and MySQL for the CM Base learning platform, and taught programming with Scratch, Minecraft Education, and Python.

## Projects

### Low-latency exchange and matching engine

C++. May 2025 to present.

A NASDAQ-style exchange built from scratch. It has a matching engine with auctions and pre-trade risk checks, an event-sourced journal, and spec-exact ITCH 5.0 and OUCH messaging over MoldUDP64 and SoupBinTCP-style transport with A/B feed arbitration. It publishes full-depth, top-of-book, snapshot, and drop-copy feeds.

- The limit order book went from 310 ns to 42 ns median per message, about 18M messages per second on one core with real ITCH data. That took 14 measured experiments. I checked correctness against a reference implementation with differential fuzzing over more than 2 billion generated operations.
- An AF_XDP kernel-bypass path, benchmarked against epoll, busy-polling, and io_uring across separate cloud instances using NIC hardware timestamps. Tick-to-trade came in at 14 µs p50 and 38 µs p99, which is 3.1× lower p99 than epoll. End to end it scales to 4.2M messages per second on 8 cores with NUMA-aware symbol sharding.
- A deterministic simulation harness that puts time, network, and disk behind interfaces. A seeded single-threaded simulator injects packet loss, reordering, partitions, crashes, and disk stalls. It has found 23 bugs so far, and every one reproduces from its seed.
- Hot-standby failover through state machine replication, with takeover under 50 ms and no lost or duplicated fills. The failover and session-recovery protocol is specified in TLA+, and the lock-free SPSC and MPSC queues are model-checked with GenMC.
- A NanoLog-style binary logger that costs about 9 ns per call on the hot path. It writes compact binary entries and formats them offline.

### ExeTrade

Python, pandas, NumPy, asyncio, ib_insync, XGBoost, AWS EC2. February 2026 to present.

A fully automated equity trading system that I built and operate on my own. It trades real capital on Interactive Brokers.

- A watchdog-supervised engine with a crash-safe, idempotent fill ledger and continuous reconciliation of broker positions against the internal book. It runs on EC2 under PM2, and a Telegram bot handles alerts.
- An independent clean-room backtester that re-implements the production engine and reconciles to it within 0.2 percentage points of CAGR, plus a monitor that compares live trading to the backtest. Removing an O(N²) hot path made backtests 11× faster.
- An SEC EDGAR XBRL fundamentals pipeline with 96.5% coverage and 98.6% accuracy on an 8,419-event walk-forward holdout. It corrects vendor fundamentals in real time and checks for drift against each quarterly WRDS refresh.
- The research behind it covers a long-only momentum, value, and quality strategy on point-in-time, survivorship-bias-free S&P 1500 data with leakage controls. There are 60 numbered, logged experiments, including a long stretch with XGBoost rankers that the live strategy no longer uses.

### Trade capture system

Java, Spring Boot, Kafka, QuickFIX/J. May 2025 to present. Built with a team of 8 in Agile sprints.

An event-driven microservices system for trade capture, corrections, and cancellations with real-time validation, modeled on an investment bank's middle-office workflow.

- A FIX execution engine on QuickFIX/J. After profiling showed database writes were the bottleneck, batching JPA writes and tuning Kafka partitioning raised throughput 3×, from 2,000 to 6,000 messages per second.
- Services sit behind OAuth 2.0 with audit logging and deploy on Kubernetes through Jenkins CI/CD.
- A React and Next.js dashboard for watching trades in real time.

### Travel Tracker

Flask, PostgreSQL, SQLAlchemy, Leaflet. Started April 2025.

A web app for logging trips and viewing travel history on interactive maps. It includes a small recommendation service that combines collaborative filtering, content embeddings, and geospatial clustering, and answers in under 200 ms.

### Apex Cluster

Python. 2022 to 2023.

My high school capstone. It grouped more than 300 students into presentation sessions based on their interests, using K-means with preference weighting. The school's administration used it for scheduling, and it matched student preferences 35% better than random assignment.

## Skills

Languages: Python, C++, Java, TypeScript, JavaScript, SQL, Dart

Backend and infrastructure: Spring Boot, Kafka, gRPC/Protobuf, Flask, asyncio, QuickFIX/J, OAuth 2.0, Docker, Kubernetes, Jenkins, AWS, Linux, Git, MySQL, PostgreSQL, Snowflake

Front end: React, Redux, Next.js, Flutter

Data and ML: pandas, NumPy, XGBoost, LLM function calling, RAG and embedding search

## Contact

Not everything above is public. If you'd like to see something that isn't, or just want to talk, email me at michaelslyang@gmail.com. When I'm not at a keyboard I'm usually on a golf course.
