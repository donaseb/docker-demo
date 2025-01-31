Docker Networking

Docker networking allows containers to communicate with each other and with the host system. There are different networking scenarios and types of Docker networks that manage container connectivity securely and efficiently.

Scenarios

Scenario 1: Containers Should Communicate with Each Other

When two containers (e.g., Container 1 and Container 2) need to talk to each other, they must be on the same network.

A bridge network can be used to allow communication between them.

Scenario 2: Containers Should Be Isolated from Each Other

If two containers (e.g., a login container and a finance container) need to be isolated, they should be placed on separate networks.

A custom bridge network should be used to enhance security.

Understanding Docker Networking

Default Network and Virtual Ethernet Interfaces

The host system has a default network interface (e.g., eth0).

Containers also have their own virtual network interfaces.

If containers and the host system are on different networks, they cannot communicate directly.

To enable communication, Docker creates a virtual Ethernet interface that connects the container to the host.

Types of Docker Networks

1. Bridge Networking (Default Network - docker0)

This is the default network created by Docker.

Containers within the same bridge network can communicate with each other.

If a container is on docker0, it can connect to the host.

2. Host Networking

Containers directly use the host’s network.

Docker binds the container to the same subnet or CIDR block as the host.

Eliminates the network isolation between the host and container.

3. Overlay Networking

Commonly used in Kubernetes and Docker Swarm.

Used when managing multiple hosts within a cluster.

Provides a common network for all hosts in the cluster.

Essential when deploying applications across multiple networks.

Custom Bridge Network for Enhanced Security

By default, containers communicate with the host using eth0.

If a container does not require strict security (e.g., a frontend container), it can remain on the default docker0 network.

Containers requiring security (e.g., finance services) should use a custom bridge network.

The custom bridge network isolates sensitive containers and ensures secure communication.

Creating a Custom Network in Docker

Create a custom network:

docker network create my_custom_network

Run a container with the custom network:

docker run --net my_custom_network -d my_secure_container

This ensures that sensitive containers use a separate, secure path while still allowing necessary communication.

By using Docker network commands, we can manage container communication and isolation efficiently.

![image](https://github.com/user-attachments/assets/fe8b1dac-5e1d-4983-8445-b3abf4176f11)
running the nginx in detached mode
here conatiner1 is the login container
now log into the container
![image](https://github.com/user-attachments/assets/598f51dc-002c-4e74-ace0-6f61e8f6ecae)
# apt update
install ping 
#sudo apt-get update
sudo apt-get install iputils-ping -y
create another contsiner logout 
![image](https://github.com/user-attachments/assets/1c426493-e9a5-434e-ae95-82daa63ddec6)
to know the ip adress of the conatiner use 
docker inspect login-new
here ip adrres is 172.17.0.3
![image](https://github.com/user-attachments/assets/25b59349-3f9c-4ed7-b180-dc8239ded307)
ip adress of logout-new is 172.17.0.4
![image](https://github.com/user-attachments/assets/953104d5-cfd9-45de-b5f3-e3bf4e381101)
here we used default bridge network so both of the conatiners should be in same subnet
when u ping one conatiner form other both works can be accese
***![image](https://github.com/user-attachments/assets/afcd975a-330a-42e1-bfbb-e8b4771d10f4)
network here in both containers are bridge nework
![image](https://github.com/user-attachments/assets/1902dc70-5294-47d8-848c-f88ca7b2be3e)
shows brige ,host netwrok






