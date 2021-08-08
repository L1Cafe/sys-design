# Describe DNS

DNS stands for Domain Name System. It is a distributed database that allows the resolution of human-readable hostnamesinto IP addresses, but it can have other targets, such as other hostnames.

## How DNS is organised

There exists a [set of Top-Level Domains](https://en.wikipedia.org/wiki/List_of_Internet_top-level_domains) (TLDs).

Originally, only seven TLDs existed. As the Internet expanded internationally, country-specific TLDs were introduced. Today, there are thousands of TLDs including company-specific ones such as [.aws](https://nic.aws) or [.deloitte](https://home.deloitte).

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

# Extra knowledge

The below points, while related to DNS, are not necessarily required knowledge for an experienced engineer, but it depends on your area.

## LANs: mDNS Bonjour, and the .local TLD

[Bonjour](https://en.wikipedia.org/wiki/Bonjour_(software)), by Apple, is one of the most well-known zero-conf networking technologies.

The [.local TLD](https://en.wikipedia.org/wiki/.local) is 

## Security: DNS amplification DDOS attack

