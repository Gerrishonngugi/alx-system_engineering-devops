Explanation of Each Component
Firewalls:

Purpose: Firewalls are used to protect each segment of the infrastructure by filtering incoming and outgoing traffic based on predetermined security rules. They help prevent unauthorized access and potential attacks.
Placement:
One firewall in front of the load balancer to filter all incoming traffic.
One firewall in front of each web server to further protect and isolate the servers.
One firewall in front of the database to secure the database server from direct access.
SSL Certificate:

Purpose: An SSL certificate is used to encrypt traffic between the user's browser and the web server, ensuring data security and privacy.
Usage: This certificate will be installed on the load balancer to serve the website over HTTPS (e.g., https://www.foobar.com).
Monitoring Clients:

Purpose: Monitoring clients are installed on each server to collect data on system performance, resource usage, and application health. They help in detecting issues early and maintaining optimal performance.
Data Collection: Monitoring tools like Sumologic collect data such as CPU usage, memory usage, disk I/O, network traffic, application logs, and database performance. This data is sent to a centralized monitoring system for analysis and alerting.
Additional Elements and Their Roles
HTTPS Traffic:

Purpose: Serving traffic over HTTPS ensures that data transferred between the user's browser and the web server is encrypted, protecting it from eavesdropping and tampering.
Monitoring:

Purpose: Monitoring is used to track the health and performance of the infrastructure. It provides visibility into system metrics, helps in identifying bottlenecks, and allows for proactive issue resolution.
QPS Monitoring: To monitor Queries Per Second (QPS) on the web server, you can set up metrics collection for the number of HTTP requests handled by the web server. Monitoring tools can be configured to track this metric and alert administrators if it exceeds certain thresholds.
Issues with This Infrastructure
Terminating SSL at the Load Balancer:

Issue: If SSL termination is done at the load balancer, traffic between the load balancer and the web servers is unencrypted. This can be a security risk, especially if the traffic travels over an insecure network.
Solution: Consider using end-to-end encryption by encrypting traffic between the load balancer and the web servers as well.
Single MySQL Server for Writes:

Issue: Having only one MySQL server capable of accepting writes creates a single point of failure for write operations. If this server goes down, no write operations can be performed.
Solution: Implement a MySQL master-slave or master-master replication setup to distribute write operations and provide redundancy.
Homogeneous Servers:

Issue: If all servers have the same components (web server, application server, and database), it can lead to resource contention and complexity in management. It's also less efficient in terms of scaling and resource utilization.
Solution: Separate concerns by dedicating specific servers for web, application, and database roles. This allows for independent scaling and more efficient resource allocation.
