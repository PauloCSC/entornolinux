---
# try also 'default' to start simple
theme: seriph
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/1819616/programming
background: https://source.unsplash.com/collection/1819616/1920x1080
# apply any windi css classes to the current slide
class: 'text-center'
# https://sli.dev/custom/highlighters.html
highlighter: shiki
# show line numbers in code blocks
lineNumbers: false
download: true
# some information about the slides, markdown enabled
info: |
  ## Taller de Entorno Linux
  Slides for general public.

  By. Joseph M. & Paulo S.
---

# Taller de Entorno a Linux

Sesión #2: Configuración de un Entorno de Desarrollo

---
layout: image-right
image: https://source.unsplash.com/collection/12013352/1920x1080
class: text-center
---

<br><br><br><br>

# Tuning our Linux Environment
<br>

Requeriments:

Any distribution with GUI

Preferably based on debian

---
layout: default
---


<div class="grid grid-cols-2 gap-x-4">
<div>

# Vi / Vim / NeoVim

Instalación
```bash
sudo apt install vi
sudo apt install vim
sudo apt install neovim
```
Uso básico
```bash
vi <pathtoFile> # Abrir un archivo
```

Cheat Sheet

https://gist.github.com/m3nd3s/3959966

Plugins

https://vimawesome.com/

</div>
<div>


# Visual Studio Code

Instalación
```bash
wget "https://code.visualstudio.com/sha/download?build=stable&os=linux-deb-x64" -O code.deb && sudo dpkg -i code.deb && rm code.deb
```
Uso básico
```bash
code <pathtoFile>   # Abrir un archivo
code <pathtoFolder> # Abrir un folder
```

Extensiones
<img src="https://box.misaelabanto.com/Screenshot_1.png" class="justify-center w-40">

</div></div>

---

# Configurando conexiones remotas

Utilizaremos el servicio SSH para poder acceder remotamente a nuestro servidor

<div class="grid grid-cols-2 gap-x-4">
<div>

- Editando la condiguracion de SSH
  ```bash
  vi /etc/ssh/sshd_config
  ```
  Descomentar la siguiente linea para indicar el puerto de nuestro servicio
  ```bash
  ...
  # port 22
  ...
  ```
  (Opcional) Cambiar el valor de la siguiente linea por YES
  ```bash
  ...
  PermitRootLogin NO # to PermitRootLogin YES
  ...
  ```
</div>
<div>

- Habilitando los puertos en el firewall
```bash
# Debian/Ubuntu - UFW
sudo ufw allow 22/tcp
# IPTables
sudo /sbin/iptables -A INPUT -m state --state NEW -m tcp -p tcp --dport 22 -j ACCEPT
# CentOS/Fedora/RedHat
sudo firewall-cmd --permanent --zone=public --add-port=22/tcp
sudo firewall-cmd --reload
```
- Iniciando el servicio

```bash
sudo service ssh restart     # Debian/Ubuntu
sudo systemctl restart ssh   # Debian/Ubuntu

sudo service sshd restart    # CentOS/Fedora/RedHat
sudo systemctl restart sshd  # CentOS/Fedora/RedHat
```
</div>
</div>

---

# Asegurando las conexiones
Crearemos y utilizaremos llaves publicas para conectarnos a nuestro servidor

<div class="grid grid-cols-2 gap-x-4">
<div>
🚨 En nuestro cliente

- Creando llave pública y privada
```bash
ssh-keygen -t rsa # Comando para crear par de llaves
```
<br>

- Verificando el par de llaves
```bash
cd ~/.ssh/ # cd C:\Users\<user>\.ssh\
ls 
```
<br>

- Cambiando permisos de archivos
```bash
chmod 600 id_rsa
```
</div>
<div>
🚨 En nuestro servidor

- Copiando nuestra llave pública
```powershell
# Powershell Syntax
Get-Content C:\Users\<user>\.ssh\id_rsa.pub
```
```bat
:: CMD Syntax
type  C:\Users\<user>\.ssh\id_rsa.pub
```
```bash
# Bash Syntax
cat ~/.ssh/id_rsa.pub
```
- Registrando nuestra llave publica
```bash
vi ~/.ssh/authorized_keys
# En este archivo debemos copiar el 
# contenido de nuestra llave pública
```

</div>
</div>

---

# Probando nuestras conexiones
Probaremos la conexión remota y configuraremos formas rápidas para conectarnos

<div class="grid grid-cols-2 gap-x-4">
<div>

- Conexion típica por SSH

  ```bash
  ssh -p <puerto> -i <llave_privada> user@ip-server
  ssh -p <puerto> -i <llave_privada> user@hostname
  ```
  Por ejemplo:
  ```bash
  ssh -p 2222 -i id_rsa test@192.168.12.20
  ssh -i id_rsa test@database.contoso.com
  ```

</div>
<div>

- Agilizando futuras conexiones

```bash
touch ~/.ssh/config     # Creamos el archivo
chmod 600 ~/.ssh/config # Modificamos permisos
```

Ejemplos de contenido
```bash
Host dev
  HostName dev.example.com
  User john
  Port 2322
Host 192.166.123.23
  HostName 192.166.123.23
  User root
  Port 2021
  IdentityFile ~/.ssh/id_rsa
```
</div>
</div>

---



<div class="grid grid-cols-2 gap-x-4">
<div>

# Tmux

Tmux ➪ Es un multiplexor de terminal

- Instalación
  > sudo apt install tmux
- Configuración
  ```bash
  cd
  git clone https://github.com/gpakosz/.tmux.git
  ln -s -f .tmux/.tmux.conf
  cp .tmux/.tmux.conf.local .
  ```
- Uso básico

  Prefix: <kbd>Ctrl + a</kbd> o <kbd>Ctrl + b</kbd>

- Cheat Sheet: https://tmuxcheatsheet.com/

</div>
<div>
<br><br><br><br><br><br><br><br><br><br><br>
<img src="https://cloud.githubusercontent.com/assets/553208/19740585/85596a5a-9bbf-11e6-8aa1-7c8d9829c008.gif">


</div>
</div>

---

# Trabajando con Dockers - VS Code

<img src="https://box.misaelabanto.com/Remote-VSCode.png" class="w-450">
<br>
<div class="grid grid-cols-2 gap-x-4">
<div>
<img src="https://box.misaelabanto.com/Containers-VSCode.png" class="w-250">
</div>
<div>
<img src="https://box.misaelabanto.com/SSH-VSCode.png" class="w-250">
</div>
</div>


