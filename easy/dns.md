# Describe DNS

DNS stands for Domain Name System. It is a distributed database that allows the resolution of human-readable hostnames into IP addresses, but it can have other targets, such as other hostnames.

## How DNS is organised

There exists a [set of Top-Level Domains](https://en.wikipedia.org/wiki/List_of_Internet_top-level_domains) (TLDs).

Originally, only seven TLDs existed. As the Internet expanded internationally, country-specific TLDs were introduced. Today, there are thousands of TLDs including company-specific ones such as [.aws](https://nic.aws) or [.deloitte](https://home.deloitte).

There is a list of [root servers](https://www.internic.net/domain/named.root). This file is called "root hints", and lets DNS servers locate the servers that contain the full [root zone](http://www.internic.net/domain/root.zone).

The root zone contains a list of TLDs and the IP address of the server that holds the registry for that TLD. Each TLD also signs the next TLD in alphabetical order, this can be seen with the `NSEC` and `RRSIG` entries on this file. This is called a [trust anchor](https://en.wikipedia.org/wiki/Domain_Name_System_Security_Extensions#Trust_anchors_and_authentication_chains). 

## How DNS queries work

Most Internet users don't connect directly to root servers in order to retrieve records. Not only this would be slow, but also nearly impossible to scale at the size of the modern Internet. Instead, multiple layers of caching are used.

### Step 1

Local hosts file. This file typically located on `/etc/hosts` on Unix machines and `C:\Windows\System32\Drivers\etc\hosts` on Windows computers, contains local, static definitions of computers, usually located in the same LAN as the machines operate. This is actually the earliest implementation of DNS. DNS servers are a relatively modern invention.

### Step 2

ISP or OS' configured DNS server. If the step above is unable to find the domain name, the OS generates a query for its configured DNS servers to answer. These can be the famous `8.8.8.8` from Google, `1.1.1.1` from CloudFlare, `9.9.9.9` from Quad9, or simply your ISP's DNS server, which tend to be the fastest due to physical network proximity. It could be the case that, for high-traffic sites (think Amazon, Google, Facebook, Twitter), your ISP actually has the domain name cached because a user previously requested the same domain name you're trying to access. If this is the case, the ISP will return the result directly from memory. If that is not the case, the DNS server will search for the Top-Level Domain DNS server. It may be necessary to query a DNS root nameserver in this step. The query contains the TLD; for example, `.com`, `.net`, or `.ru`.

### Step 3

We're back at your OS' preferred DNS server. After finding the Top-Level Domain DNS location, this server will make another request to the TLD DNS server. The query contains the domain. For example, `facebook.com`, or `mit.edu`.

### Step 4

The last server to query is the called the authoritative nameserver. This nameserver contains the definition of the Fully-Qualified Domain Name (FQDN). For example, `www.google.com` (notice the `www.` at the front, called a "subdomain", part of the `google.com` domain), or `smile.amazon.co.uk`. With the information obtained on step 3, the OS' preferred DNS server can now query the authoritative nameserver and receive the final answer.

### Step 5

Finally, with the FQDN resolved, the OS' preferred DNS server returns the information to the client. The information received contains a translation from the hostname into the requested record type. Typically, A for IPv4 and AAAA for IPv6 addresses.

## A close look at a DNS packet

There are two kinds of DNS packets: Questions (queries) and answers (responses). DNS is a UDP-based protocol, servers are available to accept DNS queries on the well-known port 53/UDP.

### Question packet

```
                                    1  1  1  1  1  1
      0  1  2  3  4  5  6  7  8  9  0  1  2  3  4  5
    +--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+
    |                                               |
    /                     QNAME                     /
    /                                               /
    +--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+
    |                     QTYPE                     |
    +--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+
    |                     QCLASS                    |
    +--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+
```

The question packet contains the domain name (for example `www.apple.com`), the type of query (more information below), and the class of the query. Typically "Internet addresses".

### Answer packet

```
                                    1  1  1  1  1  1
      0  1  2  3  4  5  6  7  8  9  0  1  2  3  4  5
    +--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+
    |                                               |
    /                                               /
    /                      NAME                     /
    |                                               |
    +--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+
    |                      TYPE                     |
    +--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+
    |                     CLASS                     |
    +--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+
    |                      TTL                      |
    |                                               |
    +--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+
    |                   RDLENGTH                    |
    +--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--|
    /                     RDATA                     /
    /                                               /
    +--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+
```

The answer contains the domain name used in the question, the type and class again, the TTL which specifies the maximum time in seconds this record should be cached for, the length for `RDATA`, and, finally, `RDATA` is the answer to the initial query. The format of `RDATA` depends on the type of resource requested.


## DNS record types

## DNSSEC

When DNS was introduced, in ARPANET, the entire network was considered trustworthy. Once the Internet started expanding internationally, network engineers realised it was easy to carry out high-impact attacks against DNS such as DNS spoofing (more below). Because the Internet was growing at a fast pace and businesses as well as Internet users wanted a higher degree of security, DNSSEC was introduced to facilitate and standarise an additional layer of cryptographic authentication on top of traditional DNS.

Note that DNS does not introduce encryption, it only provides integrity: that is, a DNS client can verify if the data was tampered with by a malicious third-party upon receiving a DNS request, but it doesn't protect this client from eavesdropping.

When a DNSSEC-secured domain is queried, every response to a DNS lookup will contain a cryptographic signature of the resource requested, along with the resource itself. To verify the signature, it is enough to find the public key published through a DNSKEY record.

## DNS spoofing

DNS spoofing is also known as DNS cache poisoning. In order to carry this out, an attacker can trick a DNS server into accepting a response from a non-legitimate DNS server. This can be achieved by means of [Man-In-The-Middle attacks](https://en.wikipedia.org/wiki/Man-in-the-middle_attack) among others. Following the steps above, the attacker would insert itself between any of the steps. Typically, an attacker can insert itself into networks with low security levels such as those found in homes or small businesses. Once any computer in the network requests a domain name, the attacker intercepts the response, and replies with addresses of machines it controls. This can allow an attacker to perform additional Man-In-The-Middle attacks, for example, by spoofing the victim's bank website.

# Extra knowledge

The below points, while related to DNS, are not necessarily required knowledge for an experienced engineer, but it depends on your area.

## LANs: mDNS, Bonjour, and the .local TLD

[Bonjour](https://en.wikipedia.org/wiki/Bonjour_(software)), by Apple, is one of the most well-known zero-conf networking technologies.

The [.local TLD](https://en.wikipedia.org/wiki/.local) is a special-use domain name that cannot be served over the Internet.

With the introduction of [RFC6762](https://datatracker.ietf.org/doc/html/rfc6762), Apple designed a protocol (called mDNS, and implemented as "Bonjour" in their computers) that allows systems on a network to exchange hostnames without the need for a centralised DNS infrastructure.

An mDNS message is a [multicast](https://en.wikipedia.org/wiki/Multicast) UDP packet sent to:
- IPv4 address 224.0.0.251 or IPv6 address ff02::fb
- UDP port 5353
- When using Ethernet frames, the standard IP multicast MAC address 01:00:5E:00:00:FB (for IPv4) or 33:33:00:00:00:FB (for IPv6)

The questions and answers follow a similar structure to the DNS protocol.

## Security: DNS amplification DoS attack

A DNS amplification attack exploits implementation flaws in open DNS resolvers in order to send massive amounts of network traffic to a victim host. Because of the way TCP/IP is implemented, hosts use a queue to listen to incoming packets. The queue is decreased by one every time a server software responds to a connection. For example, when you try connecting via HTTP to a web server, the first packet is held by the OS, while it informs the web server that there's a new connection pending. Once the web server accepts it, the OS will remove that packet from the queue, and it's the web server that will reply to the client.

Usually, requests are accepted within microseconds, but if the amount of traffic is higher than what the host's can process, then the queue will eventually get full and the OS will begin dropping packets, which prevents legitimate users from being able to connect (Denial-of-Service).

In order to carry this out, the attacker sends UDP packets to DNS servers that have the origin IP changed to be the target victim's host. In these packets, the attacker specifies the DNS server to retrieve all the information it has, in order to generate the maximum amount of traffic. This packet is then sent to the target victim, which enters the queue.

With only a single DNS server it is not likely this would pose a problem, but these attacks work by leveraging hundreds of DNS servers, and it quickly becomes a problem once the target victim receives hundreds of packets it didn't expect to receive. This is why it's called "DNS amplification", as the queries are much smaller than the responses from the DNS server. This allows an attacker with limited resources to carry out highly effective DoSes.
