### Custom Step-by-Step Guide for Reinstallation with MAAS on Fresh Ubuntu Server 24

Based on your request and the provided resources, here’s a comprehensive plan for your **Ubuntu Server 24 with MAAS integration** utilizing your storage devices and maintaining the operational structure you envision. I’ve included adjustments for Ghost-based mirroring and SEO optimization plans, as well as the future implementation of your dockerized Aether network.

---

### **High-Level Objectives**
1. **Setup and Partitioning**:
   - Use your 500GB SSD for the OS and primary services.
   - Secure OPNsense on the 256GB M.2 SSD for firewall and VPN.
   - Optimize storage on the 12TB HDD, 3TB HDD, and 5TB portable HDD for data, backups, and media repositories.
   - Assign the 1TB USB SSD for critical and fast-access application data.

2. **MAAS Installation**:
   - Install MAAS for provisioning and managing nodes (physical and virtual).
   - Prepare and manage Dockerized applications for WordPress, Nextcloud, Drupal, Laravel, and Ghost.

3. **Custom Networking and Security**:
   - Integrate OPNsense as the primary security layer for all operations.
   - Harden all systems with SSL, firewalls, and isolated Docker networks.

4. **Ghost SEO and Mirror Optimization**:
   - Set up Ghost containers for your primary content delivery and mirrored domain reflection.

5. **Documentation**:
   - Track all setups in Jupyter notebooks for transparency and reproducibility.

---

### **Preparation Checklist**
1. Backup any critical data on your existing drives to a secure external source.
2. Gather:
   - Ubuntu Server 24 ISO.
   - OPNsense ISO (for M.2 SSD installation).
   - Docker Compose files (`docker-compose.yml` from your `Master Code Framework`).
3. Prepare a secondary machine for remote management (optional but ideal).

---

### **Step 1: Install Ubuntu Server 24**
1. **Boot and Install Ubuntu**:
   - Use the 500GB SSD for installation.
   - Allocate `/` (root) partition (200GB), `/home` (150GB), and `/swap` (16GB). Keep 134GB unallocated for flexibility.

2. **Update and Upgrade**:
   ```bash
   sudo apt update && sudo apt upgrade -y
   ```

---

### **Step 2: Prepare Drives for Data Storage**
1. **Partition and Mount Drives**:
   - Format and mount your drives as follows:
     - **12TB HDD**: `/mnt/aether`
     - **3TB HDD**: `/mnt/media`
     - **5TB Portable HDD**: `/mnt/portable`
     - **1TB USB SSD**: `/mnt/fast-access`

   Example commands:
   ```bash
   sudo mkfs.ext4 /dev/sdb
   sudo mkdir -p /mnt/aether
   sudo mount /dev/sdb1 /mnt/aether
   ```

2. **Edit `/etc/fstab`** to ensure persistence:
   ```bash
   UUID=<drive-uuid> /mnt/aether ext4 defaults 0 2
   ```

---

### **Step 3: Install and Configure MAAS**
1. **Install MAAS**:
   ```bash
   sudo apt install maas -y
   sudo maas init
   ```

2. **Configure Networking**:
   - Assign a static IP to the MAAS controller.
   - Enable DHCP and DNS for node management in MAAS.

3. **Access MAAS Web UI**:
   - Visit `http://<server-ip>:5240/MAAS` and complete initial setup.

4. **Add Storage Pools**:
   - Integrate your 12TB and 3TB drives as MAAS storage pools for provisioning.

---

### **Step 4: Deploy OPNsense on the M.2 SSD**
1. **Install OPNsense**:
   - Boot into the OPNsense installer using your 256GB M.2 SSD.
   - Configure OPNsense for:
     - WAN to LAN routing.
     - DNS filtering.
     - OpenVPN setup.

2. **Link OPNsense to MAAS**:
   - Assign MAAS nodes static IPs using OPNsense DHCP reservations.

---

### **Step 5: Set Up Docker Environment**
1. **Install Docker and Compose**:
   ```bash
   sudo apt install docker.io docker-compose -y
   ```

2. **Deploy Applications Using `docker-compose.yml`**:
   - Use the `Master Code Framework` file to configure services like:
     - MariaDB, Nextcloud, WordPress, Drupal, Laravel, and Ghost.

   Example:
   ```bash
   cd /mnt/aether/docker-backend
   docker-compose up -d
   ```

3. **Set Up Proxy and SSL**:
   - Configure NGINX proxy and Let’s Encrypt for public domains:
     - `nextcloud.omniversal.cloud`
     - `wordpress.omniversal.cloud`
     - `ghost.omniversal.cloud`

---

### **Step 6: Mirror Ghost for SEO Optimization**
1. **Primary Ghost Setup**:
   - Deploy Ghost using the provided `docker-compose.yml`.
   - Configure environment variables (`.env.ghost`) to match your public domains.

2. **Ghost Mirror Setup**:
   - Create a secondary Ghost instance with unique content identifiers.
   - Cross-link with your main domains for enhanced SEO.

---

### **Step 7: Document Everything in Jupyter Notebooks**
1. Install Jupyter:
   ```bash
   sudo apt install python3-pip
   pip3 install jupyter
   ```

2. Organize Configurations:
   - Store all system logs, configurations, and steps in notebooks within `/mnt/aether/docs`.

---

### **Step 8: Test and Finalize**
1. Verify:
   - Nodes provisioned by MAAS.
   - Applications running smoothly in Docker.
   - Ghost SEO functionality.

2. Harden Security:
   - Enable UFW firewall:
     ```bash
     sudo ufw enable
     sudo ufw allow 22,80,443/tcp
     ```

3. Backup:
   - Use the 5TB portable drive for snapshots and `/etc` backups.

---

### **Next Steps**
- Let me know if you'd like deeper focus on any specific component (e.g., SEO scripting, Docker setup, or MAAS troubleshooting).  
- Confirm when you're ready to proceed—I’ll guide you through each segment live or provide detailed sub-steps as needed.
