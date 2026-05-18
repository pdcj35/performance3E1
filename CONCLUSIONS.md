# Conclusions: Performance Testing (FakeStore API)

*Date:* May 2026  
*Target:* Authentication Endpoint (POST /auth/login)
*Status:* Passed

---

## Results:

| Metric | Target (SLA) | Actual Result | Status |
| :--- | :--- | :--- | :--- |
| *Throughput* | Constant 20 TPS | *20.2 TPS* | 🟢 Passed |
| *Response Time* | Max 1500 ms | *95th Percentile (P95) < 280 ms* | 🟢 Passed |
| *Error Rate* | < 3% | *0.00%* | 🟢 Passed |

- This is a load testing running over the fakestor API, when a user login the website, API response with a 201 status code and generate an access token. After running the load test, system worked as expected and is aligned with all the required conditions
- This load testing could be performed with dynamic data, because of it was configured to use the user and password data from a .csv file
- In the future the endpoint could be subjected to stress or soak testing, since the system respond very well with a 20 TPS, it could be escalated to more users, also soak testing could be useful to see the API behavior after a long time performance
