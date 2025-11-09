<div align="center">

# 📦 PAQUETES Y EXTRAS ADICIONALES

### Software opcional y herramientas útiles para Arch Linux + KDE Plasma

<img src="https://img.shields.io/badge/Paquetes-1000+-blue?style=for-the-badge" alt="Paquetes"/>
<img src="https://img.shields.io/badge/Flatpak-Soportado-green?style=for-the-badge&logo=flathub" alt="Flatpak"/>
<img src="https://img.shields.io/badge/AUR-Yay-orange?style=for-the-badge&logo=archlinux" alt="AUR"/>

</div>

---

## 📋 CONTENIDO

<table width="100%">
<tr>
<td width="50%" valign="top">

**📦 Gestores de paquetes**
- [Flatpak](#-flatpak)
- [AUR Helper (yay)](#-aur-helper-yay)

**🖥️ Hardware**
- [Desktop](#desktop)
- [Laptop](#laptop)
- [Bluetooth](#bluetooth)
- [Impresoras](#impresoras)

</td>
<td width="50%" valign="top">

**🎮 Software**
- [Gaming](#-gaming)
- [Desarrollo](#-desarrollo)
- [Multimedia](#-multimedia)
- [Herramientas](#️-herramientas-del-sistema)

</td>
</tr>
</table>

---

<div align="center">

## 📦 FLATPAK

<img src="https://flathub.org/img/logo/flathub-logo-toolbar.svg" width="200px"/>

<img src="https://img.shields.io/badge/Apps-2000+-success?style=flat-square" alt="Apps"/>
<img src="https://img.shields.io/badge/Universal-Linux-blue?style=flat-square" alt="Universal"/>

</div>

### 📖 ¿Qué es Flatpak?

<table>
<tr>
<td>

Sistema de **paquetes universales** para Linux. Útil para:

- ✅ Apps no disponibles en repos oficiales
- ✅ Última versión de software
- ✅ Sandboxing (seguridad)
- ✅ Actualizaciones independientes del sistema

</td>
</tr>
</table>

### 🔧 Instalación

```bash
# Instalar Flatpak
sudo pacman -S flatpak

# Añadir Flathub (repositorio oficial)
flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo

# Reiniciar para integración completa
reboot
```

### 🔧 Comandos útiles

<table>
<tr>
<th>Comando</th>
<th>Descripción</th>
</tr>
<tr>
<td><code>flatpak list</code></td>
<td>Listar apps instaladas</td>
</tr>
<tr>
<td><code>flatpak update</code></td>
<td>Actualizar todas las apps</td>
</tr>
<tr>
<td><code>flatpak uninstall APP</code></td>
<td>Desinstalar app</td>
</tr>
<tr>
<td><code>flatpak run APP</code></td>
<td>Ejecutar app</td>
</tr>
<tr>
<td><code>flatpak uninstall --unused</code></td>
<td>Limpiar apps no usadas</td>
</tr>
</table>

---

<div align="center">

## 🔧 AUR HELPER (YAY)

<img src="https://img.shields.io/badge/AUR-Yay-1793D1?style=for-the-badge&logo=archlinux&logoColor=white" alt="Yay"/>

</div>

### 📖 ¿Qué es AUR?

<table>
<tr>
<td width="60%">

**Arch User Repository** es un repositorio mantenido por la comunidad.

**Ventajas:**
- 📦 Miles de paquetes adicionales
- 🚀 Software propietario (Chrome, Spotify, VS Code)
- 🔧 Herramientas específicas
- 🎮 Temas y personalizaciones

</td>
<td width="40%">

```bash
# Buscar
yay -Ss nombre

# Instalar
yay -S paquete
```

</td>
</tr>
</table>

### 🔧 Instalación de yay

```bash
# Instalar dependencias
sudo pacman -S git base-devel

# Clonar repositorio
mkdir -p /home/$USER/tmp
cd /home/$USER/tmp
git clone https://aur.archlinux.org/yay.git

# Compilar e instalar
cd yay
makepkg -si

# Verificar
yay --version
```

### ⚠️ Seguridad

<table>
<tr>
<td>

**IMPORTANTE:** Siempre revisa el PKGBUILD antes de instalar:

```bash
yay -G paquete  # Descargar PKGBUILD
cd paquete
less PKGBUILD   # Revisar contenido
```

</td>
</tr>
</table>

---

<div align="center">

## 🖥️ HARDWARE ESPECÍFICO

</div>

### Desktop

<details>
<summary><b>🖥️ Optimizaciones para PC de escritorio</b></summary>

<br>

```bash
# BIOS/UEFI utils
sudo pacman -S efibootmgr os-prober

# CPU Microcode (mejora estabilidad)
sudo pacman -S amd-ucode   # Para AMD
sudo pacman -S intel-ucode # Para Intel

# Sensores de temperatura
sudo pacman -S lm_sensors
sudo sensors-detect
```

</details>

### Laptop

<details>
<summary><b>💻 Herramientas para portátiles</b></summary>

<br>

```bash
# Multi-monitor
sudo pacman -S kscreen

# Control de brillo
sudo pacman -S brightnessctl

# TLP (optimización batería)
sudo pacman -S tlp tlp-rdw
sudo systemctl enable tlp
sudo systemctl start tlp

# PowerDevil (ya debería estar)
sudo pacman -S powerdevil
```

**Uso de brightnessctl:**
```bash
brightnessctl set 50%       # 50% brillo
brightnessctl set +10%      # Aumentar 10%
brightnessctl set 10%-      # Reducir 10%
```

</details>

### Bluetooth

<details>
<summary><b>📡 Configuración Bluetooth</b></summary>

<br>

```bash
# Stack completo
sudo pacman -S bluez bluez-utils bluedevil

# Activar servicio
sudo systemctl enable --now bluetooth

# GUI adicional (opcional)
sudo pacman -S blueman
```

**Uso CLI:**
```bash
bluetoothctl
[bluetooth]# power on
[bluetooth]# scan on
[bluetooth]# pair XX:XX:XX:XX:XX:XX
[bluetooth]# connect XX:XX:XX:XX:XX:XX
```

</details>

### Impresoras

<details>
<summary><b>🖨️ Configuración de impresoras</b></summary>

<br>

```bash
# CUPS (sistema de impresión)
sudo pacman -S cups print-manager

# Activar servicio
sudo systemctl enable --now cups

# Drivers comunes
sudo pacman -S hplip         # HP
sudo pacman -S gutenprint    # Epson, Canon
```

**Configuración web:** http://localhost:631

</details>

---

<div align="center">

## 🎮 GAMING

<img src="https://img.shields.io/badge/Steam-000000?style=for-the-badge&logo=steam&logoColor=white" alt="Steam"/>
<img src="https://img.shields.io/badge/Proton-Enabled-success?style=for-the-badge" alt="Proton"/>

</div>

### 🎮 Steam

```bash
# Instalar Steam
sudo pacman -S steam

# Drivers 32-bit según GPU
# Intel:
sudo pacman -S lib32-mesa lib32-vulkan-intel

# AMD:
sudo pacman -S lib32-mesa lib32-vulkan-radeon

# NVIDIA:
sudo pacman -S lib32-nvidia-utils
```

### 🕹️ Otros launchers

<table>
<tr>
<th>Launcher</th>
<th>Instalación</th>
</tr>
<tr>
<td>Lutris (Epic, GOG, emuladores)</td>
<td><code>sudo pacman -S lutris wine-staging</code></td>
</tr>
<tr>
<td>Heroic (Epic/GOG)</td>
<td><code>yay -S heroic-games-launcher-bin</code></td>
</tr>
</table>

### ⚡ Optimizaciones gaming

<details>
<summary><b>🚀 GameMode (boost rendimiento)</b></summary>

<br>

```bash
sudo pacman -S gamemode lib32-gamemode

# Uso en Steam: Añadir a opciones de lanzamiento
gamemoderun %command%
```

</details>

<details>
<summary><b>📊 MangoHud (overlay FPS)</b></summary>

<br>

```bash
sudo pacman -S mangohud lib32-mangohud

# Uso:
mangohud %command%

# Variable global
echo "MANGOHUD=1" >> ~/.bashrc
```

</details>

---

<div align="center">

## 💻 DESARROLLO

<img src="https://img.shields.io/badge/VSCode-007ACC?style=for-the-badge&logo=visualstudiocode&logoColor=white" alt="VSCode"/>
<img src="https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white" alt="Docker"/>
<img src="https://img.shields.io/badge/Git-F05032?style=for-the-badge&logo=git&logoColor=white" alt="Git"/>

</div>

<div align="center">

## 🎨 MULTIMEDIA

</div>

### 🖼️ Edición de imagen

```bash
# GIMP
sudo pacman -S gimp

# Inkscape (vectorial)
sudo pacman -S inkscape

# Krita (dibujo)
sudo pacman -S krita
```

### 🎬 Edición de vídeo

```bash
# Kdenlive (ya instalado)
sudo pacman -S kdenlive

# DaVinci Resolve
yay -S davinci-resolve
```

### 🎵 Audio

```bash
# Audacity
sudo pacman -S audacity

# Ardour (DAW)
sudo pacman -S ardour

# EasyEffects
sudo pacman -S easyeffects
```

---

<div align="center">

## 🛠️ HERRAMIENTAS DEL SISTEMA

</div>

### 💾 Particiones

```bash
# KDE Partition Manager (ya viene con kde-system-meta)
sudo pacman -S partitionmanager

# GNOME Disks
sudo pacman -S gnome-disk-utility
```

### 📦 Compresión

```bash
# Formatos adicionales para Ark
sudo pacman -S p7zip unrar unzip zip
```

### 📊 Monitoring

```bash
# System Monitor (ya instalado)

# Neofetch/Fastfetch
sudo pacman -S fastfetch
```

---

<div align="center">

## 📊 RESUMEN DE EXTRAS

</div>

<table width="100%">
<tr>
<th width="25%">📦 Categoría</th>
<th width="25%">✅ Esencial</th>
<th width="50%">📝 Opcional</th>
</tr>
<tr>
<td><b>Flatpak</b></td>
<td>Recomendado</td>
<td>Apps universales (Spotify, Discord)</td>
</tr>
<tr>
<td><b>yay</b></td>
<td>Muy útil</td>
<td>Acceso a AUR (Chrome, VS Code, temas)</td>
</tr>
<tr>
<td><b>Bluetooth</b></td>
<td>Si tienes hardware</td>
<td>bluez, bluedevil</td>
</tr>
<tr>
<td><b>Impresoras</b></td>
<td>Si tienes</td>
<td>CUPS, drivers HP/Epson</td>
</tr>
<tr>
<td><b>Gaming</b></td>
<td>Steam</td>
<td>Lutris, Heroic, GameMode, MangoHud</td>
</tr>
<tr>
<td><b>Desarrollo</b></td>
<td>VS Code, Git</td>
<td>Docker, lenguajes, DBs</td>
</tr>
</table>

---

<div align="center">

### [← Volver al README](../README.md)

<img src="https://raw.githubusercontent.com/catppuccin/catppuccin/main/assets/footers/gray0_ctp_on_line.svg" width="600px"/>

</div>
