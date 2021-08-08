# Describe DNS

DNS stands for Domain Name System. It is a distributed database that allows the resolution of human-readable hostnamesinto IP addresses, but it can have other targets, such as other hostnames.

## How DNS is organised

There exists a [set of Top-Level Domains](https://en.wikipedia.org/wiki/List_of_Internet_top-level_domains) (TLDs).

Originally, only seven TLDs existed. As the Internet expanded internationally, country-specific TLDs were introduced. Today, there are thousands of TLDs including company-specific ones such as [.aws](https://nic.aws) or [.deloitte](https://home.deloitte).

## How DNS queries work

## A close look at a DNS packet

## DNSSEC

When DNS was introduced, in ARPANET, the entire network was considered trustworthy. Once the Internet started expanding internationally, network engineers realised it was easy to carry out high-impact attacks against DNS such as DNS spoofing (more below). Because the Internet was growing at a fast pace and businesses as well as Internet users wanted a higher degree of security, DNSSEC was introduced to facilitate and standarise an additional layer of cryptographic authentication on top of traditional DNS. Note that DNS does not introduce encryption, it only provides integrity: that is, a DNS client can verify if the data was tampered with by a malicious third-party upon receiving a DNS request, but it doesn't protect this client from eavesdropping.

## DNS spoofing

# Extra knowledge

The below points, while related to DNS, are not necessarily required knowledge for an experienced engineer, but it depends on your area.

## LANs: mDNS Bonjour, and the .local TLD

[Bonjour](https://en.wikipedia.org/wiki/Bonjour_(software)), by Apple, is one of the most well-known zero-conf networking technologies.

The [.local TLD](https://en.wikipedia.org/wiki/.local) is 

## Security: DNS amplification DDOS attack

