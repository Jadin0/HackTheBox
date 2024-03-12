---
description: Network File System
---

# NFS

Developed by Sun Microsystems and has the same purpose as [SMB](smb.md); To access file systems over a network as if they were local.



NFSv3

* Authenticates the client device

NFSv4

* Authenticates the user



<figure><img src="../../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

A significant advantage of NFSv4 over its predecessors is that only one UDP or TCP port `2049` is used to run the service, which simplifies the use of the protocol across firewalls.



NFS protocol has `no` mechanism for `authentication` or `authorization`. Instead, authentication is completely shifted to the RPC protocol's options. The authorization is derived from the available file system information. In this process, the server is responsible for translating the client's user information into the file system's format and converting the corresponding authorization details into the required UNIX syntax as accurately as possible.



The most common authentication is via UNIX `UID`/`GID` and `group memberships`, which is why this syntax is most likely to be applied to the NFS protocol.
