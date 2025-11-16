### 🔹 Linux Firewall Configuration (iptables / nftables)
  - Configured iptables to define custom firewall rules:
    ```
    sudo iptables -P INPUT DROP
    sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT
    sudo iptables -A INPUT -p tcp --dport 80 -j ACCEPT
    sudo iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
    sudo iptables -L -v
    ```
  - Logged dropped packets for later analysis via /var/log/syslog.
  
  - Explored nftables for modern rule management and compared efficiency with iptables.
  
  - Practiced packet tracing with:
  ```
  sudo iptables -A INPUT -j LOG --log-prefix "Dropped Packet: "
  ```
  - Understood rule chains, persistence, and NAT translation.
