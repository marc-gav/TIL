# DNS exfiltration
I was solving a forensic's challenge in picoCTF that consisted of a Wireshark packet capture. Obsviously I had no clue how to move forward with the challenge because I wasn't aware of this hacking technique. This youtube explanation: https://www.youtube.com/watch?v=jDY6nW4yNBM was helpful.

DNS exfiltration consists of hiding data in DNS requests. The idea is to encode the data in the address of a DNS request. For example:
```
subdomain.domain.com -> subdomain = leaked_document_contents
leaked_document_contents.domain.com
```

Obviously it is not possible to send the entire document in a single DNS request, so the idea is to split the document in chunks and send each chunk in a different DNS request. The chunks are encoded in base64 and, in this case, the subdomain is the base64 encoded chunk.

In the CTF challenge the flag was indeed hidden in the DNS communication. I used https://gchq.github.io/CyberChef/ to decode the base64 chunks and I got the flag.
