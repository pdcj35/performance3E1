# Performance Testing - Login Service (FakeStore API)

This repository contains a performance testing project using *Apache JMeter* to simulate user load on the authentication endpoint of the FakeStore API.

## Test Scenario Criteria
- *Target Throughput:* Achieve and maintain a constant rate of at least *20 TPS*.
- *Data Parameterization:* Credentials are dynamically loaded from a .csv file.
- *Response Time:* Maximum allowed response time is *1.5 seconds*.
- *Error Rate:* Error rate must be *less than 3%* of the requests.

## JMeter Configuration Details
- *HTTP Method:* POST
- *Endpoint Route:* https://fakestoreapi.com/auth/login
- *Response Assertion:* Configured to validate a *201 Created* status code response.
- *Load Shaping:* Controlled using a Thread Group with 40 Virtual Users combined with a Constant Throughput Timer set to 1200 samples per minute to regulate the 20 TPS baseline.

## How to Run the Test
1. Clone or download this repository to your local machine.
2. Open Apache JMeter.
3. Load the .jmx test plan file included in this project.
4. Select the CSV Data Set Config element and make sure the Filename field points to the correct local path of your users.csv file.
5. Click on *Play* button to execute the test.
