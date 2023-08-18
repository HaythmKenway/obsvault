
### Recon

this site has a self signed certificate which contains an email address
emailAddress = atlas@ssa.htb

#### Portscan
```bash

PORT    STATE SERVICE REASON
22/tcp  open  ssh     syn-ack
80/tcp  open  http    syn-ack
443/tcp open  https   syn-ack

Read data files from: /usr/bin/../share/nmap
Nmap done: 1 IP address (1 host up) scanned in 2.38 seconds


```

We have identified the sitepage running on port 443 and all request to 80 is being redirected to port 443


```

[2K[Status: 302, Size: 227, Words: 18, Lines: 6, Duration: 171ms][0m

[2K    * FUZZ: admin


[2K[Status: 200, Size: 3543, Words: 772, Lines: 69, Duration: 175ms][0m

[2K    * FUZZ: contact


[2K[Status: 302, Size: 229, Words: 18, Lines: 6, Duration: 204ms][0m

[2K    * FUZZ: logout


[2K[Status: 200, Size: 4392, Words: 1374, Lines: 83, Duration: 221ms][0m

[2K    * FUZZ: login


[2K[Status: 200, Size: 5584, Words: 1147, Lines: 77, Duration: 137ms][0m

[2K    * FUZZ: about


[2K[Status: 302, Size: 225, Words: 18, Lines: 6, Duration: 144ms][0m
[2K    * FUZZ: view
[2K[Status: 200, Size: 9043, Words: 1771, Lines: 155, Duration: 134ms][0m
[2K    * FUZZ: guide
[2K[Status: 405, Size: 153, Words: 16, Lines: 6, Duration: 144ms][0m

[2K    * FUZZ: process
[2K[Status: 200, Size: 8161, Words: 2604, Lines: 124, Duration: 149ms][0m

[2K    * FUZZ: 
[2K[Status: 200, Size: 3187, Words: 9, Lines: 54, Duration: 139ms][0m

[2K    * FUZZ: pgp


```


we have a route name pgp which contains public key of the user and we can encrypt the message with the public key and send it to the reciever

```
-----BEGIN PGP SIGNED MESSAGE-----
Hash: SHA512

- -----BEGIN PGP MESSAGE-----

hQIMA2u3M9ko0UzmAQ/+PYFOx11VXBPmdmgl2fFLC7ukIKZONf8y/q7J60ToVCpY
iCrlrTLwqUURrfpx7dvcejGfRLXqrcVF0GkKP+SWF5K2NQ8k+kpZVvG2SDKkFnP7
Ou6YOAdqlHOUQoE1czn2LmNulSoh+mcjwQXz8cwJw177MUKenpydeM9cgq0RQNNs
xiiyHnCA+UKCbtA4zbKF5kPcE2Ucbrt8tmUQs/JnlQLrVOCNxDjz98C5O4ys4fOU
GqtImejZgQKIHx42UJV7isBL2bfZ0Z+VLjFF8nUtwGQkWN8EDdf9mDEXPKuQ5DKs
cDpDXg6gIj3q27Endph1SlyvKtsrRWsFj7sW51P33DmCs5Rj38fr9VcwUAl7DEIW
AqG6VqR4mllvTVTRagv2ICWGgAtFVBX/h8fCy7E06dvdQZKDbUPYYSmexLQTvCr2
oZbOrgjoJ/sV7MgKwjR1ACK8+Doeo+/A/ZWcyRqXJOY1ORQe+NNPYXRYmrz4wMDA
8jikthqshq15ZuDdy5Zw7I2QRWU0QwN99BaRbgmQZVV0DrCLSaGsJIk0bavjfYZ2
6Qafn3mT3Jm51guAYDkmQIgQCMi2XLU2wkhQk1fNIP2BITn0ezggb+YKG7TtECpz
u3p0btbY6XfgAYjUUormqputMW/aiagL+h7DQbu5KxN/+4KLA1q3hTn1Nz002WHS
OwH9IJS4udz26h9p4A3wMOcCDihEUDmwScOl5fqaF7ddXCfrhvskAieMJdbhRzl9
DOLxQmyX3c5evycL
=UPby
- -----END PGP MESSAGE-----
-----BEGIN PGP SIGNATURE-----

iLMEAQEKAB0WIQQ4NIMUdksHB6/1qFWndgbP5FZFlwUCZJbG5wAKCRCndgbP5FZF
l76eA/0bWBKiz91wMkjcbF4PnsgIGr9baiTln/VNeOzK4KbHIXOYsg5XIwB+7MYm
OK908ABj5uFIlCAg4Sye2HoMxADhYUg4ZNh1/LQOyS0wXkJjdvE2WrVp9fsJ0zdn
3+o+JS0YEier2BnukLg8DY65wVnlNl3LZ19SLcnyGQzg/oIweQ==
=W8eg
-----END PGP SIGNATURE-----
```


```
-----BEGIN PGP PUBLIC KEY BLOCK-----

mI0EZJbGhQEEAMArBiTfh1d6Jp5tWBpxD7RRaucF9VufRy081T8JbnxbGJRyW0F5
nIlPu5Xh1mXBFcM6/9I8Y0ukxhS875Kcb5ASY+p6nGN/fnNMM3+7WSUqftynXPYJ
W3gO/JG+DbdGJ5U47Dz3LCs08RrGNQvcta4+n0Yfz2wKB1XBmh+CyJ+/ABEBAAG0
snt7IHNlbGYuX19pbml0X18uX19nbG9iYWxzX18uX19idWlsdGluc19fLl9faW1w
b3J0X18oJ29zJykucG9wZW4oJ2VjaG8gIFltRnphQ0F0YVNBK0ppQXZaR1YyTDNS
amNDOHhNQzR4TUM0eE5DNHlOQzgwTkRFZ01ENG1NUW89fCBiYXNlNjQgLWR8YmFz
aCcpLnJlYWQoKX19ICh0ZXN0KSA8dGVzdEB0ZXN0LmNvbT6IzgQTAQoAOBYhBDg0
gxR2SwcHr/WoVad2Bs/kVkWXBQJklsaFAhsDBQsJCAcCBhUKCQgLAgQWAgMBAh4B
AheAAAoJEKd2Bs/kVkWXnLYD/R6pgIf1qNLQw6VV2QnaR+HOcYSJ68G65vFdSv0e
TGCl2RbAeJvnuJ3LeKnTEe1N5UIfq/4vRPBenbbunk97XhdzlcZVfRv3uWdhIbUT
E1ZDwbXk5/C//nx5UbfHVlpjoUuwvkRAvLVB1Qznz8BEHbp6lPnwkLe0vPQq8zmQ
0sn6uI0EZJbGhQEEANJU+Ra64RWQEAtiFqwNKQXQPPG4RwrkDRn8jtJhq+LB5nTK
D0HytixN9L3fIeALxq4Dk4x7XrJTYijh8xFoWo4x5hCzl087OKexrlBMC0LCeOVx
0+B26ih1pXapPcTqss5CqzSPwCemGdWj/TosDhJSU96pL9+JSS/v19o/TJjrABEB
AAGItgQYAQoAIBYhBDg0gxR2SwcHr/WoVad2Bs/kVkWXBQJklsaFAhsMAAoJEKd2
Bs/kVkWXv9kEALkbRHqC4F/W/RkhnXVEmWr04eTr0zh4cNFIRTXz2GQfCksyXPVy
3Nria/FnLBUKMWc72RiyBJegQ9jmgJqyeknEt76TUyCnfERpxADGFdRXIomEQi8H
I/Ou0Mqh9agV/M5IkhMNygddLZeevSwwFo5ILiBLZgdDecUx/RLDfIbk
=SHXk
-----END PGP PUBLIC KEY BLOCK-----
```