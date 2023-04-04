# assignment-1-part-4

# Step-1 Create a new Docker network named "my_network" using the bridge driver.

# Command To Exec
docker network create --driver bridge my_network

# Output
4c8229f9af4cd3facad8abc9fb937583cf46ec43d1350614280495714760a2f2

# What The Command Is
bridge driver is used to create an internal network that allows containers to communicate with each other.

# Step-2 Create a new Docker container using the "nginx" image and connect it to the "my_network" network. Name the container "nginx_container".

# Command To Exec
docker run -d --name nginx_container -p 8080:80 --network my_network nginx

# Output
22137bbe73b23a3a661d5e45719f02177c7f64a1a46ba693091fa122f91b14bc

# What The Command Is
This command creates a new Docker container using the "nginx" image and connects it to the "my_network" network. The "-d" flag specifies that the container should be started in detached mode, which means it will run in the background. The "--name" flag specifies the name of the container as "nginx_container".

# Step-3 Verify that the "nginx" default page is accessible on your host machine at http://localhost:8080

Browsed and its working.

# Step-4 Create a new Docker container using the "httpd" image and connect it to the "my_network" network. Name the container "httpd_container".

# Command To Exec
docker run -d --name httpd_container --network my_network -p 8081:80 httpd

# Output
3c8136713440f590142626a3f9361aa2849658475034b68466dad7f3901397a4

# What The Command Is
This maps port 80 of the container to port 8081 of your host, allowing you to access the "httpd" default page at http://localhost:8081.

# Step-5 Verify that the "httpd" default page is accessible on your host machine at http://localhost:8081.

Browsed and its working - It Work showed Up on Webpage.

# Step-6 Use the "docker network inspect" command to display information about the "my_network" network. Document your findings in the README.md file.

# Command To Exec
docker network inspect my_network

# Output
[
    {
        "Name": "my_network",
        "Id": "4c8229f9af4cd3facad8abc9fb937583cf46ec43d1350614280495714760a2f2",
        "Created": "2023-03-31T19:22:35.593012378+05:00",
        "Scope": "local",
        "Driver": "bridge",
        "EnableIPv6": false,
        "IPAM": {
            "Driver": "default",
            "Options": {},
            "Config": [
                {
                    "Subnet": "172.18.0.0/16",
                    "Gateway": "172.18.0.1"
                }
            ]
        },
        "Internal": false,
        "Attachable": false,
        "Ingress": false,
        "ConfigFrom": {
            "Network": ""
        },
        "ConfigOnly": false,
        "Containers": {
            "22137bbe73b23a3a661d5e45719f02177c7f64a1a46ba693091fa122f91b14bc": {
                "Name": "nginx_container",
                "EndpointID": "38aa4de157b77d8064a8e621a4678eae72e94229a8bb3d0e210e5493c71c3b45",
                "MacAddress": "02:42:ac:12:00:02",
                "IPv4Address": "172.18.0.2/16",
                "IPv6Address": ""
            },
            "3c8136713440f590142626a3f9361aa2849658475034b68466dad7f3901397a4": {
                "Name": "httpd_container",
                "EndpointID": "54838bb35b42b2c5c3d3b23749b0970c2d75f2eb6e0d470e06e7a763736d3c4f",
                "MacAddress": "02:42:ac:12:00:03",
                "IPv4Address": "172.18.0.3/16",
                "IPv6Address": ""
            }
        },
        "Options": {},
        "Labels": {}
    }
]

# What The Command Is
Display information about the "my_network" network, such as its name, ID, and a list of connected containers.

# Step-7 Stop and remove the "nginx_container" container.

# Command To Exec
docker stop nginx_container && docker rm nginx_container

# Output
nginx_container
nginx_container

I browsed that if we can run two seperate commands together and found yes this can be via && so tested on this one.

# Step-8 Create a new Docker container using the "nginx" image and connect it to the "my_network" network. Name the container "nginx_container_2

# Command To Exec
docker run -d --name nginx_container_2 -p 8082:80 --network my_network nginx

# Output
b7f5c567b1f7752e2b35a65df9cb1057aa442e55c37041640617760f9d9e0bcb

This was the same step as step 2 but just needed to change the port to 8082 and name to _2.

# Step-9 Verify that the "nginx" default page is accessible on your host machine at http://localhost:8082

Browsed and it is working.

# Step-10 Use the "docker container ls" command to display information about all running containers.

# Command To Exec
docker container ls

# Output
CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS          PORTS                                       NAMES
b7f5c567b1f7   nginx     "/docker-entrypoint.…"   4 minutes ago    Up 4 minutes    0.0.0.0:8082->80/tcp, :::8082->80/tcp       nginx_container_2
3c8136713440   httpd     "httpd-foreground"       16 minutes ago   Up 16 minutes   0.0.0.0:8081->80/tcp, :::8081->80/tcp       httpd_container
7674669c05ec   myapp     "docker-entrypoint.s…"   3 hours ago      Up 3 hours      3000/tcp                                    5c2ac7e4cc40
5c2ac7e4cc40   myapp     "docker-entrypoint.s…"   3 hours ago      Up 3 hours      0.0.0.0:3000->3000/tcp, :::3000->3000/tcp   abdul_basit

# Step-11 Stop and remove all containers.

# Command To Exec
docker stop $(docker ps -aq) && docker rm $(docker ps -aq)

# Output
a6ffe495515c
9e63763eac68
5f4d997e2fbb
1b0912791476
3aa1942dea3b
4d00cae45800
0c026041f86c
b079662b44db
d5a4b60bf840
a58390a109c5
6499e45f94f6
1abb5f4b2613
0374ff525d00
d4179f09fb68
77be1db138e3
5c2ac7e4cc40

# What The Command Is
As i created quite many containes and didnt knew all names or id so wanted to have a solution that does the required at once for this the query found.

This command first stops all running containers by using docker stop $(docker ps -aq) 
and then removes all stopped containers by using docker rm $(docker ps -aq).

# Step-12 Cleanup

# Command To Exec
docker network rm my_network

# Output
my_network 
