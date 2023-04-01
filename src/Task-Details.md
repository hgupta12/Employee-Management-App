## Task 1

1. Created a Dockerfile
2. Changed config/database.yml
3. Built the docker image - `docker build -t iris-systems-task .`
4. Created a network - `docker network create iris-systems-task-app`
5. Ran a mysql container connected to the network - `docker run -d --network iris-systems-task-app --network-alias mysql -v iris-app-data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=password mysql:latest`
6. Ran the iris-systems-task container - `docker run -p 3000:3000 --network iris-systems-task-app iris-systems-task`

The application runs successfully!