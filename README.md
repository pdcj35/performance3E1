# Performance Testing - Login Service (FakeStore API)

This repository contains a practical performance testing project developed using *Apache JMeter* to simulate user load on the authentication endpoint of the FakeStore API.

## Test Scenario Criteria
- *Target Throughput:* Achieve and maintain a constant rate of at least *20 TPS* (Transactions Per Second).
- *Data Parameterization:* Input credentials are dynamically loaded from a .csv file.
- *Response Time SLA:* Maximum allowed response time is *1.5 seconds* (1500 ms).
- *Error Rate SLA:* Acceptable error rate must be strictly *below 3%* of the total requests.

## JMeter Configuration Details
- *HTTP Method:* POST
- *Endpoint Route:* https://fakestoreapi.com/auth/login
- *Response Assertion:* Configured to validate a successful *201 Created* status code response.
- *Load Shaping:* Controlled using a Thread Group with 40 Virtual Users (VUs) combined with a Constant Throughput Timer set to 1200 samples/minute to regulate the 20 TPS baseline.

## How to Run the Test
1. Clone or download this repository to your local machine.
2. Open Apache JMeter.
3. Load the .jmx test plan file included in this project.
4. Select the CSV Data Set Config element and make sure the Filename field points to the correct local path of your usuarios.csv file.
5. Click the green *Start* (Play) button to execute the test.