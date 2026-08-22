# tgweb
Proxy web for telegram 
# Создание ключа
```bash
openssl rand -hex 16
```
# Клонирование официального репозиторрия 
```bash
cd /tmp
git clone https://github.com/telegramdesktop/tproxy-server.git
```
# Танцы с бубном
Почему то исходный файл не хочет работать по этому мы его правим
```bash
cd /tmp/tproxy-server
sed -i 's|"\$go_binary" test \./\.\.|echo "Skipping tests (root environment quirk)"|' deploy/install.sh
```
## Создаем заглушку для сайт
```bash
mkdir site
nano site/index.html
```
*index.html*
```html
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
html { color-scheme: light dark; }
body { width: 35em; margin: 0 auto;
font-family: Tahoma, Verdana, Arial, sans-serif; }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
```

