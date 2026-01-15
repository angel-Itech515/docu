```bash
ipconfig
ipconfig /all
arp -a
route print
tracert 192.168.1.15

# Route tables
route delete 192.168.1.15 mask 255.255.255.255 192.168.6.10 
route -p delete 192.168.1.15 
route add 192.168.1.15 mask 255.255.255.255 192.168.6.254 metric 1
```

