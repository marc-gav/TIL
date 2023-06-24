Watching this video provided me with some insights into analyzing the traffic coming from a botnet attack over TCP: `https://www.youtube.com/watch?v=jFJMt-y6ZvU`

Insights:
- The delta time between packages received has to be reasonable
- You can map the IP addresses to geographical locations, display them on a map and see where the attacks are coming from.
- The initial (random) sequence number that the attacker sends on the first packet is 32 bits long. Range is [0, 2^32 - 1] = [0, 4294967295]. If 0's and 1's are randomly set the number will be on average quite large. If the number looks too small, it is suspicious.
- You can find out which ports that attacker has found open on your device by locking at your `SYN & ACK` responses.
- You can find out how far is the attacking machine from your device by looking at the `TTL` field in the `IP` header. It can be faked, but similar `TTL`s from different IPs may indicate a single machine spoofing multiple IP addresses. `TTL` typically start at 255, 128 or 64. Additionally, different operating systems use different initial `TTL`s:
    - Linux: 64
    - Windows: 128
    - Routers and switches: 255
- Nmap can find what OS a certain IP is running by sending packets to the target machine and analyzing the bits in the responses. This technique is also known as `TCP/IP` stack fingerprinting: `https://nmap.org/book/man-os-detection.html`
- Nice exercise to learn more Wireshark filters: `https://tryhackme.com/room/wiresharkfilters`
