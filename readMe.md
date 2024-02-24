Architecture Diagram Explanation:

1. The architecture has been divided into two AZ to maintain high availability, in case of a disaster our architecture and shift to the second AZ to present service outage, also the second AZ help in elevating the load by having it distributed across the region

2. Application servers are deployed with auto scaling so they may scale up and down according to the load received.

3. Elastic Cache for redis has been deployed along side both servers to cache frequently accessed data to both reduce load on the RDS and improve response time.

4. An RDS Cluster has been deployed with multi-zone deployment to ensure HA. In case of a disaster the read replica will be promoted to master. Also auto scaling has been enabled for RDS as well to improve performance.

5. A proxy for RDS instances has been deployed to pool connections to RDS and improve performance, also the proxy ensures that all read requests are redirected to the replica nodes, ensuring that only put, patch, and delete request are directed to the master node.

6. S3 bucket has been deployed to manage all image, media, and irregular files to ensure there volume does not impede RDS performance. Also a CDN has been deployed along side the S3 bucket to improve performance for clients trying access media content from all around the world

Database Schema:

1. User schema contains user data
2. Friends list is stored as a separate table that has a composite key made up of the user who has added an individual as a friend and the user who has been added as a friend
3. User and Posts have a 1 to Many relation where a post can belong to only one user but a user can have multiple posts
4. Also the number of likes received on a post is de-normalized to improve perform when getting the number of likes
