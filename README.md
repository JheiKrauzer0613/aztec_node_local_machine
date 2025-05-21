# aztec_node_local_machine
Guide on how to set-up and run aztec node using local computer if behind NAT/CGNAT network via reverse tunnel method.

# IMPORTANT: Understanding about NAT / CGNAT network
**PLEASE MAKE SOME TIME TO READ AND UNDERSTAND. YOU CANNOT FIX A PROBLEM IF YOU DON'T KNOW WHAT THE PROBLEM IS IN THE FIRST PLACE.**<br /><br />
# What is NAT (Network Address Translation)?
**NAT (Network Address Translation)** is a common networking setup where your router allows multiple devices in your home or office to share a single public IP address to access the internet. This means your computer running an Aztec node has a private IP address that isn’t directly visible from the internet, which can prevent other nodes from connecting to it.

**To fix this, you need to set up port forwarding on your router.** Port forwarding opens a specific port and directs incoming internet traffic to your node, making it reachable from outside your local network.

In short, **NAT hides your node behind your router, and port forwarding acts like opening a door so others can connect to it.**

**However, opening port forwarding alone does not guarantee reliable connectivity.** You also need a **static public IP address** from your ISP to ensure your node’s address doesn’t change over time, keeping it consistently reachable. Most users behind NAT are assigned **dynamic public IPs**, which can change periodically **unless** they request a static IP—usually for an additional cost.

## How to Test if You Are Behind NAT

### 1. Find your local (private) IP address:

- **On Windows**:  
  Open Command Prompt and type:
```ipconfig```

- **On Mac/Linux**:  
Open Terminal and type:
```ifconfig``` or ```ip addr```

- Look for your **IPv4 address**.  
If it starts with one of the following, it’s a private IP:
- `192.168.x.x`
- `10.x.x.x`
- `172.16.x.x` to `172.31.x.x`

### 2. Find your public IP address:

Visit a website like [whatismyip.com](https://whatismyip.com) to see your public IP.

### 3. Compare the two IPs:

If your local IP is a private IP and is different from your public IP, then you are **behind NAT**. <br /><br />

---

# What is CGNAT (Carrier Grade Network Address Translation)?

**Carrier-Grade NAT (CGNAT)** is a type of Network Address Translation used by Internet Service Providers (ISPs) to conserve public IPv4 addresses. Instead of assigning a unique public IP to every customer, the ISP assigns **private IP addresses** to customer routers and shares a **single public IP address** among many users.

This means that **even if you set up port forwarding on your own router, incoming connections may still be blocked at the ISP level** because you're not directly exposed to the public internet.

---

## Why CGNAT Matters for Running a Node

If you're behind CGNAT, other nodes **cannot directly connect to your Aztec node**, even if you've configured everything correctly on your router. This can prevent you from participating fully in decentralized networks that require inbound connections.

---

## How to Test if You Are Behind CGNAT

### 1. Check your router’s **WAN IP address**:

- Log in to your router’s admin dashboard.
- Look for the **WAN IP** or **Internet IP** — this is the address your ISP assigns to your router.

### 2. Compare it to your public IP address:

- Visit [whatismyip.com](https://whatismyip.com) or search “what is my IP” on Google to see your **public IP**.

### 3. Analyze the result:

- If your router’s **WAN IP is in one of these private ranges**, you are behind CGNAT:
  - `100.64.0.0` to `100.127.255.255` (CGNAT reserved range)
  - `10.0.0.0` to `10.255.255.255`
  - `172.16.0.0` to `172.31.255.255`
  - `192.168.0.0` to `192.168.255.255`

- If your **router’s WAN IP** is private and different from your public IP, then **you are behind CGNAT or double NAT**.

---

## What to Do If You're Behind NAT / CGNAT

- **Contact your ISP** and ask if they can assign you a **public static IP address** (may require a business plan or monthly fee).
- Alternatively, consider using a **reverse tunnel or relay server** to bypass NAT / CGNAT and allow inbound connections. **-- which I will guide you to set up.**






