# confluence
## Quick Start
```
git clone https://github.com/bharatmicrosystems/confluence.git
cd confluence
kubectl apply -f confluence.yaml
```
This would perform the following steps
1. Create a persistent volume called confluence-pv-volume with a path to /kubevolumes/confluence_data. This would ensure that the confluence-data is persisted on disk even if the confluence container goes down. The disk is replicated across all the nodes so the container can be scheduled to any of the nodes in the cluster
2. Create a persistent volume claim called confluence-pv-claim which binds with confluence-pv-volume
3. Create the confluence deployment which contains a reference to the official confluence container provided by atlassian and the /confluence-data volume mounted to confluence-pv-claim.
4. Create a cluster IP service to expose the confluence UI to the kubernetes cluster
5. Create an ingress service to expose the confluence UI to the outside world on confluence.example.com on port 80.

## Further setup
Access confluence from the browser and follow on-screen instructions.

Forward and paste the license key

When prompted for choosing the type of configuration, choose "Configure everything myself"

In the database-configuration choose my own database, use database PostgreSQL (ensure that you have already setup a postgres instance by using https://github.com/bharatmicrosystems/postgres.git)
1. Hostname - postgres-jiraconfluence-service
2. Port - 5432
3. Database - confluence2db
4. User - confluence2dbuser

Choose Jira database for user access and add jira-service:8080 and confluence-service:8090 as server urls
