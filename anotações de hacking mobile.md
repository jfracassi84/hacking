# Anotações de hacking mobile

## Conexão com ADB

```shell
adb connect IP:PORTA #conecta no ip:porta

adb devices #lista os devices

adb shell settings put global http_proxy IP:PORTA (Burp) #cria o proxy no android via terminal

script convert-burp-cert.sh #script para converter o certificado do burp para leitura do android
```

### convert-burp-cert.sh - Convert Burp Suite certificate to Android

```shell
openssl x509 -inform DER -in burp_cacert.der -out burp_cacert.pem
CERTHASHNAME="`openssl x509 -inform PEM -subject_hash_old -in burp_cacert.pem | head -1`.0"
mv burp_cacert.pem $CERTHASHNAME #Correct name
```

### script push-burp-cert.sh

```shell
adb root && sleep 2 && adb remount #Allow to write on /syste
adb push $CERTHASHNAME /sdcard/ #Upload certificate
adb shell mv /sdcard/$CERTHASHNAME /system/etc/security/cacerts/ #Move to correct location
adb shell chmod 644 /system/etc/security/cacerts/$CERTHASHNAME #Assign privileges
adb reboot #Now, reboot the machine
```

### Lista os certficados

```shell
adb shell ls -ltr system/etc/security/cacerts/
```

## Interceptação de requisições com Frida

### Instalação do client

```shell
pip3 install frida-tools
pip3 install objection

frida --version
```

### Instalação do server

```shell
mv frida-server-version frida-server
adb push frida-server /data/local/tmp
adb shell "chmod 755 /data/local/tmp/frida-server
adb shell "/data/local/tmp/frida-server &"
```

### Comandos básicos

```shell
frida-ps --help
frida-ps -U
frida-ps -Ua
frida-ps -Uai
frida -U "name"
frida -U -f identifier
frida -U -p PID
frida -l script.js
frida-trace -U identifier -i "open*"
frida-trace -U -p PID -i "open*"
```

### SL Pinning Bypass

```shell
Download do apk https://www.apkmirror.com/apk/x-corp/twitter
adb install -r name.apk
configure Burp to intercept the traffic
bypass SSL Pinning via https://codeshare.frida.re/@akabe1/frida-multiple-unpinning/

adb root
adb shell "/data/local/tmp/frida-server &"

frida-ps -Ua
frida --codeshare akabe1/frida-multiple-unpinning -U -p "PID do X/Twitter"
```

### Gerenciamento de arquivos

```shell
adb shell pm list packages -f -3 #lista os pacote
adb pull /caminho/do/arquivo.apk #baixa o arquivo
unzip arquivo.apk
```

### Explorar Activities Exported

```shell
adb shell am start com.example.package/.className
adb shell am start "[data]" com.example.package/.className
adb shell am start –a [action] –c [category] com.example.package/.className
```

### Explorar Exported Services

```shell
adb shell am startservice com.example.package/.className
```

### Exposed Broadcast Receivers

* Extract the source code from the AndroGoat APK
* Open “AndroidManifest.xml”
* $DIR/resources/AndroidManifest.xml
* Find the exported activity that has an “intent-filter” or attribute “android:exported” set to “true”
* Open the AndroGoat app
* Open a user shell with ADB
* Broadcast to the receiver using “am”
* am broadcast -n "…"
* Quickly check your device’s screen
* Extract the sensitive information from the Toast message

* com insegureshop

```shell
adb shell am broadcast -a mybroadcast -n com.example.myapp/.MyClass -es number 1234
```

### Exploração Deep Links

* Extract the source code from the AndroGoat APK
* Open “AndroidManifest.xml”
* $DIR/resources/AndroidManifest.xml
* Search for Deep Links starting with "scheme:" in the AndroidManifest.xml
* Figure out how to use the defined links, and start / exploit them via adb commands, like the below one:

```shell
adb shell am start -W "[schema]://[host]/[path]?[queryparm]=[value]"
```
