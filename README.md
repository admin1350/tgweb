# Гайд по поднятию прокси для телеграмм через протокол WEB

# Требования для сервера:
- Свободный 80 и 443 порт
- Статический ip желательнр
# 1. Создание ключа, через который будут подключаться устройства
```bash
openssl rand -hex 16
```
# 2. Клонирование официального репозиторрия 
```bash
cd /tmp
git clone https://github.com/telegramdesktop/tproxy-server.git
```
# 3. Исправление багов в скрипте
При попытке установить без данной правки будет возникать данная ошибка
<img width="993" height="205" alt="изображение" src="https://github.com/user-attachments/assets/3138587e-304e-4c8c-81af-6f57e8a6e79c" />

```bash
cd /tmp/tproxy-server
sed -i 's|"\$go_binary" test \./\.\.|echo "Skipping tests (root environment quirk)"|' deploy/install.sh
```
# 3. Создание сайта заглушки

```bash
mkdir /tmp/tproxy-server
nano /tmp/tproxy-server/site/index.html
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
# 4. Запуск установки и правка прав на директории
```bash
sudo ./deploy/install.sh \
  --hostname test1.sysadmin.name \
  --email admin@lord-mikrotik.ru \
  --site-dir ./site
```
тут вводим dd(ваш ключ) который был сделан(то что не пишется какой ключ это нормально)
## 4.1 Исправление прав 
Исправьте права на всю цепочку директорий
```bash
sudo chmod 755 /opt
sudo chmod -R 755 /opt/MTProxy
sudo chown -R mtproxy:mtproxy /opt/MTProxy
```
# 5. Перезапуск всех служб 
```bash
sudo systemctl restart tproxy-server
sudo systemctl restart mtproxy
sudo systemctl restart caddy
```
Подключаемся и не забываем про `dd`:
https://t.me/webproxy?server=proxy.example.org&secret=dd(Ваш ключ)
