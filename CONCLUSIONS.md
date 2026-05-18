# Post-Execution & Conclusions Report: Performance Testing (FakeStore API)

*Date:* May 2026  
*Role:* QA Performance Testing Engineer  
*Target Objective:* Authentication Endpoint (POST /auth/login)

---

## 1. Execution Summary vs SLAs
After configuring and executing the planned load scenario using Apache JMeter, the predefined Service Level Agreements (SLAs) for the core authentication workflow were validated against the actual results:

* *Throughput:* The targeted requirement was to establish and maintain a constant baseline of *20 TPS. By utilizing a *Constant Throughput Timer (calibrated to 1200 samples/minute) alongside a pool of 40 active virtual users, the transaction rate stabilized precisely at *20.2 TPS*, successfully meeting the concurrency target.
* *Response Times:* The maximum allowed response time SLA was set to *1.5 seconds (1500 ms). Throughout the entire sustained load injection, performance metrics remained optimal, recording a 95th Percentile (P95) below **280 ms*. The system demonstrated highly efficient access verification.
* *Error Rate:* The target acceptance criteria required an error rate strictly below *3%. The final test execution yielded a **0.00% error rate*, successfully fulfilling 100% of the injected transactions.

---

## 2. Key Technical Findings and Insights

### A. Stateless REST Architecture Behavior (Status Code 201 vs 200)
A critical engineering checkpoint occurred during the script development regarding response validation criteria. Initially, sample requests were flagged as failures because the automation framework anticipated a standard 200 OK success token. However, auditing the underlying raw network response streams revealed that the FakeStore API implements strict RESTful resource conventions: upon processing a successful login, it creates an active authentication token resource, natively responding with a *201 Created* status code.
Updating the Response Assertion criteria to match this native 201 success status resolved the false negatives, stabilizing the execution tree entirely.

### B. Dynamic Data Parameterization
The CSV Data Set Config component seamlessly parsed and mapped dynamic runtime credentials (usernames and passwords) directly into the JSON request body payload. This strategy neutralized backend caching biases and verified that the system adequately processes concurrent requests under completely variable data inputs in real time.

---

## 3. Future Testing Recommendations

1.  *Execute an Accelerated Stress Test:* Since the API absorbed the 20 TPS workload with exceptional response time margins and zero errors, the true physical boundaries of the infrastructure remain unmapped. It is highly recommended to scale virtual user counts exponentially in a future iteration to locate the architecture's true maximum breaking point.
2.  *Conduct an Extended Endurance Evaluation (Soak Testing):* A prolonged execution window (e.g., 1 to 2 consecutive hours) should be scheduled to guarantee that continuous, high-density JWT token issuance does not introduce backend memory leaks or exhaust database connection pool resources over extended operational cycles.