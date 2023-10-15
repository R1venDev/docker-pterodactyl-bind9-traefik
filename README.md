# docker-pterodactyl-bind9-traefik
Unlock hosting power with my guide. Set up Docker, Traefik, Bind9, and SSL for a secure, scalable environment, featuring Pterodactyl Panel.

# **Complete Docker Guide: Deploying Pterodactyl Panel with Traefik, Bind9, and SSL Certificates**

## **Foreword**

Greetings,

I'm excited to introduce you to this guide, which is not just a technical manual but also a result of my personal journey in navigating the complexities of hosting environments.

What motivated me to write this guide? While exploring YouTube, I came across several video tutorials created by different people, all focused on topics like bind9, Traefik, and Pterodactyl. However, these tutorials often had some shortcomings, and I found myself facing significant challenges and frustrations while trying to follow their instructions. My journey was marked by a lot of trial and error, and I had to work hard to overcome the problems that came up as I tried to use the guides provided by these creators.

Through determination and effort, I managed to overcome these difficulties and solve the issues that arose while following the instructions of these creators. In the end, I realized that there was a need for a more detailed and user-friendly guide that would help bridge the gaps and provide a smoother experience for those who want to understand and use bind9, Traefik, and Pterodactyl.

That's how this guide came into being — a reimagining of those previous tutorials, with improvements to make the process smoother. I'm sharing this guide to offer a comprehensive resource that simplifies the intricacies of working with bind9, Traefik, and Pterodactyl.

My goal is to help you avoid the struggles I faced and enable you to dive right into creating a hosting environment that suits your needs. Whether you're a beginner taking your first steps or an experienced enthusiast looking for a more user-friendly approach, this guide is designed to empower you on your hosting journey.

Towards the end of this guide, you'll find a section where I will provide links to video tutorials, websites, and authors that I used as references while creating this guide. This way, you can explore further and delve deeper into the topics that interest you.

So, together, let's embark on this adventure with a guide that not only provides technical knowledge but also shares the lessons I've learned from my own experiences.

Best regards, Riven.

## **Introduction**

Welcome to a comprehensive guide on setting up Pterodactyl Panel with Docker, Traefik, Bind9, and SSL certificates. This guide is designed to help you navigate the process of establishing a robust hosting environment for your applications and services. It places particular emphasis on Pterodactyl Panel, a widely-used game server management platform.

Whether you're an experienced system administrator or a newcomer looking to explore containerization and web server management, this guide offers clear, step-by-step instructions to assist you in achieving your objectives. By the time you've completed this guide, you'll have a fully functional hosting platform characterized by enhanced security, effortless scalability, and the capability to manage game servers with ease.

Before we delve into the technical details, let's briefly outline the essential components of this setup:

- **Docker**: We will make extensive use of Docker, a robust containerization platform that allows us to isolate and manage various elements of our hosting environment.

- **Traefik**: Traefik will serve as our reverse proxy, facilitating automatic SSL certificate provisioning and effective traffic routing for your services.

- **Bind9**: The Bind9 DNS server will be instrumental in managing domain name resolution, ensuring uninterrupted access to your hosted applications.

- **SSL Certificates**: Secure Sockets Layer (SSL) certificates will be implemented to encrypt data transmissions, thereby bolstering the security of your hosted services.

This guide assumes that you possess a basic understanding of Linux systems and are familiar with command-line operations. If Docker is new to you, fret not—we will cover the fundamentals as we proceed. So, without further delay, let's embark on this journey toward constructing a robust hosting environment.


## **Networks**

docker network create --driver bridge --subnet 10.20.0.0/16 dns-network
docker network create --driver bridge --subnet 10.30.0.0/16 proxy-network

docker compose up -d


This configuration is important for your physical server to be able to reach the local DNS server (bind9). Here are the steps:

**Step 1: Open resolved.conf for Editing**

Use a text editor to open the resolved.conf file. You can use the `nano` or `vi` editor. In this example, I'll use `nano`:

```shell
sudo nano /etc/systemd/resolved.conf
```

**Step 2: Modify resolved.conf**

Inside the resolved.conf file, you should see some comments and potentially other configuration options. To specify your local DNS server, add the following line at the end of the file:

```plaintext
DNS=10.20.3.2
```

**Step 3: Save and Exit**

- If you're using `nano`, press `Ctrl + O` to save the file, then press `Enter`. Next, press `Ctrl + X` to exit the editor.

**Step 4: Restart systemd-resolved Service**

After you've made the changes to resolved.conf, you need to restart the systemd-resolved service to apply the new configuration:

```shell
sudo systemctl restart systemd-resolved
```

**Step 5: Verify Configuration**

You can check that the DNS configuration has been applied by inspecting the resolved.conf file again:

```shell
cat /etc/systemd/resolved.conf
```

You should see the DNS entry set to 10.20.3.2.

**Step 6: Test DNS Resolution**

You can now test whether your server can resolve DNS queries using the local DNS server. You can do this by running the `nslookup` or `dig` command:

```shell
nslookup traefik-dashboard.panel.local.example.com
```

Replace "example.com" with a domain or hostname you want to look up. If the DNS resolution works, it means your server is using the specified local DNS server running in the Docker container.

That's it! Your systemd-resolved service is now configured to use your local DNS server at 10.20.3.2. This should enable your physical server to communicate with your Docker container's DNS service.




## **References**

1. https://technotim.live/posts/traefik-portainer-ssl/
2. https://github.com/techno-tim/techno-tim.github.io/tree/master/reference_files/traefik-portainer-ssl/traefik
3. https://www.youtube.com/watch?v=syzwLwE3Xq4
4. https://mpolinowski.github.io/docs/DevOps/Provisioning/2022-01-25--installing-bind9-docker/2022-01-25/
5. https://github.com/bluepuma77/traefik-best-practice/tree/main

6. https://technotim.live/posts/pterodactyl-game-server/#reverse-proxy
7. https://github.com/EdyTheCow/docker-pterodactyl