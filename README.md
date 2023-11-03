## Installing Pi-hole Web Interface on Mac Using Docker Containers

## Prerequisites

Before you begin, make sure you have the required items:

- Docker's desktop application installed on your Mac. 
- An internet connection.

- Now, these are the installation steps you must follow:
## 1. Install the Docker Desktop Application

If you haven't already installed Docker Desktop, you can download it from this link: https://www.docker.com/products/docker-desktop/


## 2. Open Terminal
Open the terminal application on your Mac. The icon should have a black screen with the >_ symbols present.

## 3. Open your Docker Application
Go to your Finder application, select Applications on the left-side, and look for a whale-like icon that is blue. Click it to open. 

## 4. Pull the PiHole Image via Docker
In the Terminal, use the following command to install the piehole Docker image:


sudo docker pull pihole/pihole

Downloads the latest piehole image to your docker installation. 

## 5. Create and Run Pi-hole Container
Now, you can create and run a Pi-hole container using the following command in your terminal. Replace user_password with your own password.


sudo docker run -d --name pihole -e ServerIP=your_host_ip_address -e TZ="Your/Timezone" -e WEBPASSWORD=user_password -p 53:53/tcp -p 53:53/udp -p 67:67/udp -p 80:80  -p 443:443  -v "$(pwd)/pihole/etc-pihole/:/etc/pihole/"  -v "$(pwd)/pihole/etc-dnsmasq.d/:/etc/dnsmasq.d/"  --dns=127.0.0.1 --dns=1.1.1.1 --restart=unless-stopped pihole/pihole

This creates a piehole container with specific configurations.

## 6. Access Pi-hole Web Interface:
Once you have confirmed your container is running, type in the following url:

http://your_host_ip_address/admin.

Replace "your_host_ip_address" with your Mac's IP address.

Login with the credentials you set when you built the container. 

Once you've logged in, the interface should look like this:
<img width="1720" alt="Screenshot 2023-11-02 at 6 47 27 PM" src="https://github.com/Walton5888/pihole.github.io/assets/110494531/e44d2f11-5726-4cbe-9ac8-9d43935ae705">

## 7. Docker-compose.yml block (Container-construction method that was not used)
This is what a docker-compose.yml block would look like for Pi-hole:


    version: '3'

    services:
  
      piehole:
  
        container_name: pihole
    
        image: pihole/pihole:latest
    
        ports:
          - "53:53/tcp"
          - "53:53/udp"
          - "67:67/udp"
          - "80:80"
          - "443:443"
    
        environment:
        TZ: 'User/Timezone' # Pick your timezone
        WEBPASSWORD: 'Passwd' # Set your password
    
        volumes:
          - './etc-pihole/:/etc/pihole/'
          - './etc-dnsmasq.d/:/etc/dnsmasq.d/'
    
        cap_add:
          - NET_ADMIN #sets admin privileges
   
        restart: unless-stopped


