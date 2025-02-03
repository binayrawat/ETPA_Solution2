Problem 2:
Scenario:
This scenario is not related to the above.
You need to deploy a web application into AWS infrastructure. This application should:
● Have the /get endpoint accessible publicly over the internet,
● Have the /post or /put endpoint accessible privately within the internal network only.
You can use the kennethreitz/httpbin docker image or any similar one. The kennethreitz/httpbin image, is a simple http service providing various endpoints to test multiple HTTP verbs such as /get, /post, /put, /delete.
Task Objectives:
Use Infrastructure as Code (IaC) to provision the cluster and deploy the app. You can use any IaC tool you want. Some resources you might consider:
●AVPC
● Proper routing/NAT.
● A Kubernetes cluster (e.g., EKS) deployed into a private subnet(s), running the kennethreitz/httpbin container. Configure at least two different endpoints: one public (GET) and one private (POST or another verb).
● Implement an Ingress or Load Balancer setup to:
• Expose the public endpoint.
• Expose the private endpoint so that it's only accessible internally.
Please also include a Readme explaining the implementation.
