## Installing Pi-hole on Mac using Docker
Prerequisites
Before you begin, make sure you have the required items:

Docker's desktop application installed on your Mac. 
An internet connection.
Installation Steps
## 1. Install the Docker Desktop Application
If you haven't already installed Docker Desktop, you can download it from this link: https://www.docker.com/products/docker-desktop/


## 2. Open Terminal
Open the terminal application on your Mac.

## 3. Pull the PiHole Image via Docker
In the Terminal, use the following command to install the piehole Docker image:


docker pull pihole/pihole
Downloads the latest piehole image to your docker installation. 

## 4. Run Pi-hole Container
Now, you can create and run a Pi-hole container using the following command. Replace your_password with your desired web interface password:


docker run -d \
    --name pihole \
    -e ServerIP=your_host_ip_address \
    -e TZ="America/California" \
    -e WEBPASSWORD=user_password \
    -p 53:53/tcp -p 53:53/udp \
    -p 67:67/udp \
    -p 80:80 \
    -p 443:443 \
    -v "$(pwd)/pihole/etc-pihole/:/etc/pihole/" \
    -v "$(pwd)/pihole/etc-dnsmasq.d/:/etc/dnsmasq.d/" \
    --dns=127.0.0.1 --dns=1.1.1.1 \
    --restart=unless-stopped \
    pihole/pihole

This creates a piehole container with specific configurations.

## 5. Access Pi-hole Web Interface:
Once you have confirmed your container is running, type in the following url:

http://your_host_ip_address/admin.

Replace "your_host_ip_address" with your Mac's IP address.

Login with the credentials you set when you built the container. 
