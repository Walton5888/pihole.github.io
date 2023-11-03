Installing Pi-hole on Mac using Docker
Prerequisites
Before you begin, make sure you have the following prerequisites:

Docker Desktop installed on your Mac.
A working internet connection.
Installation Steps
1. Install Docker Desktop
If you haven't already installed Docker Desktop, you can download it from the official Docker website and follow the installation instructions:

Docker Desktop for Mac
2. Open Terminal
Open the terminal application on your Mac.

3. Pull the PiHole Image via Docker
In the Terminal, use the following command to pull the Pi-hole Docker image from Docker Hub:


docker pull pihole/pihole
Downloads the latest piehole image to your docker installation. 

4. Run Pi-hole Container
Now, you can create and run a Pi-hole container using the following command. Replace your_password with your desired web interface password:

bash
Copy code
docker run -d \
    --name pihole \
    -e ServerIP=your_ip_address \
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
This creates a container with specific configurations.

5. Access Pi-hole Web Interface:
Once you have confirmed your container is running, type in the following url:
http://your_host_ip_address/admin.
