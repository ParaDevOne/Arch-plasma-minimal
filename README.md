<div align="center">

# 🐧 ARCH LINUX + KDE PLASMA MÍNIMO

### Guía práctica y completa desde USB hasta escritorio funcional

<p align="center">
  <img src="https://img.shields.io/badge/Arch_Linux-1793D1?style=for-the-badge&logo=arch-linux&logoColor=white" alt="Arch Linux"/>
  <img src="https://img.shields.io/badge/KDE-1D99F3?style=for-the-badge&logo=kde&logoColor=white" alt="KDE"/>
  <img src="https://img.shields.io/badge/Plasma-0095D5?style=for-the-badge&logo=kde&logoColor=white" alt="Plasma"/>
  <img src="https://img.shields.io/badge/License-MIT-green?style=for-the-badge" alt="License"/>
</p>

<p align="center">
  <strong>Última actualización:</strong> Noviembre 2025<br>
  <strong>Tiempo estimado:</strong> 45-90 minutos<br>
  <strong>Espacio en disco:</strong> ~5-8 GB
</p>

---

<img src="https://raw.githubusercontent.com/catppuccin/catppuccin/main/assets/palette/macchiato.png" width="600px" />

</div>

## 📋 CONTENIDO

<table width="100%">
<tr>
<td width="50%" valign="top">

### 🚀 INSTALACIÓN

- [📥 Fase 0: Preparación USB](#-fase-0-preparación-usb)
- [💾 Fase 1: archinstall](#-fase-1-instalación-base-con-archinstall)
- [🎉 Fase 2: Primer boot](#-fase-2-primer-boot)
- [🔧 Fase 3: Post-instalación](#-fase-3-post-instalación-manual)

</td>
<td width="50%" valign="top">

### ⚙️ CONFIGURACIÓN

- [⚡ Fase 4: Optimizaciones](./docs/optimizaciones.md)
- [📦 Fase 5: Extras](./docs/extras.md)
- [⚠️ Troubleshooting](#️-troubleshooting-común)
- [🧹 Mantenimiento](#-mantenimiento-regular)

</td>
</tr>
</table>

---

<div align="center">

## 🔥 FASE 0: PREPARACIÓN USB

</div>

### 📥 Descargar ISO oficial

<table>
<tr>
<td width="60%">

**Enlace oficial:** [Arch Linux - Downloads](https://archlinux.org/download/)

Descarga la última ISO disponible.

</td>
<td width="40%">

</td>
</tr>
</table>

### 🔐 Verificar SHA256

<details>
<summary><b>🖥️ Linux / macOS</b></summary>

```bash
sha256sum archlinux-YYYY.MM.DD-x86_64.iso
```

</details>

<details>
<summary><b>🪟 Windows (PowerShell)</b></summary>

```powershell
Get-FileHash archlinux-YYYY.MM.DD-x86_64.iso -Algorithm SHA256
```

</details>

> ⚠️ **Importante:** Comparar con el hash oficial en la web

### 💾 Crear USB booteable con Ventoy

<div align="center">
<img src="https://www.ventoy.net/static/img/ventoy.png" width="125px"/>
</div>

<details>
<summary><b>📖 ¿Qué es Ventoy?</b></summary>

<br>

**Ventoy** es una herramienta que permite crear USBs multiboot. Ventajas:

- ✅ Múltiples ISOs en el mismo USB
- ✅ Sin necesidad de reformatear
- ✅ Drag & drop de ISOs
- ✅ Compatible con BIOS/UEFI

</details>

<br>

**Pasos de instalación:**

1. **📥 Descargar:** [Ventoy - Downloads](https://www.ventoy.net/download.html)

2. **🔧 Instalar Ventoy:**

   | Sistema | Comando |
   |---------|---------|
   | Windows | Ejecutar `Ventoy2Disk.exe` como administrador |
   | Linux | `sudo sh Ventoy2Disk.sh -i /dev/sdX` |

3. **📋 Copiar ISO** directamente al USB (sin extraer)

4. **🚀 Bootear:** USB aparecerá como menú de Ventoy

### ⚙️ Configuración BIOS

<table>
<tr>
<th>⚙️ Opción</th>
<th>✅ Configuración recomendada</th>
</tr>
<tr>
<td><b>Boot Mode</b></td>
<td><code>UEFI</code> (recomendado)</td>
</tr>
<tr>
<td><b>Secure Boot</b></td>
<td><code>Disabled</code> (temporal)</td>
</tr>
<tr>
<td><b>Boot Priority</b></td>
<td><code>USB First</code></td>
</tr>
</table>

> 🎹 **Teclas de acceso:** F2 / F12 / DEL (según fabricante)

---

<div align="left">

## 💾 FASE 1: INSTALACIÓN BASE CON `archinstall`

</div>

### 1.1 🌐 Conectar a Internet

<table>
<tr>
<td width="50%">

<details>
<summary><b>📡 ETHERNET (recomendado)</b></summary>

```bash
# Conectar cable
ping -c 3 archlinux.org
```
✅ Si funciona, continúa

</details>

</td>
<td width="50%">

<details>
<summary><b>📶 WiFi</b></summary>

<br>

```
iwctl

[iwd]# device list
[iwd]# station wlan0 scan
[iwd]# station wlan0 get-networks
[iwd]# station wlan0 connect "RED"
[iwd]# exit

ping -c 3 archlinux.org
```

</details>

</td>
</tr>
</table>

### 1.2 🚀 Ejecutar archinstall

```bash
archinstall
```

### 1.3 ⚙️ Configuración recomendada

<table>
<tr>
<th width="35%">📋 Opción</th>
<th width="65%">✅ Valor recomendado</th>
</tr>
<tr>
<td>Language</td>
<td><code>Spanish</code> (o tu idioma)</td>
</tr>
<tr>
<td>Keyboard</td>
<td><code>es</code></td>
</tr>
<tr>
<td>Mirror region</td>
<td><code>Spain</code> (tu país)</td>
</tr>
<tr>
<td>Locale</td>
<td><code>es_ES.UTF-8</code></td>
</tr>
<tr>
<td>Disk configuration</td>
<td><code>Best-effort default layout</code></td>
</tr>
<tr>
<td>Filesystem</td>
<td><code>ext4</code></td>
</tr>
<tr>
<td>Encryption</td>
<td><code>No</code> (o LUKS si quieres)</td>
</tr>
<tr>
<td>Bootloader</td>
<td><code>Grub</code></td>
</tr>
<tr>
<td>Swap</td>
<td><code>True</code></td>
</tr>
<tr>
<td>Hostname</td>
<td><code>archlinux</code></td>
</tr>
<tr style="background-color:#fff3cd;">
<td><b>⚠️ Profile</b></td>
<td><b>Desktop → KDE Plasma → MINIMAL</b></td>
</tr>
<tr>
<td>Display driver</td>
<td>Intel / AMD / NVIDIA</td>
</tr>
<tr>
<td>Audio</td>
<td><code>Sin servidor de audio</code></td>
</tr>
<tr>
<td>Kernels</td>
<td><code>linux</code></td>
</tr>
<tr>
<td>Additional packages</td>
<td><code>git wget curl</code> (opcional)</td>
</tr>
<tr>
<td>Network</td>
<td><code>NetworkManager</code></td>
</tr>
<tr>
<td>Timezone</td>
<td><code>Europe/Madrid</code></td>
</tr>
<tr>
<td>Optional repos</td>
<td><code>multilib</code> (Steam/Wine)</td>
</tr>
</table>

<div align="left">

> 💡 **Tip:** Al finalizar → `Install` → **NO chrootees** → Reinicia y quita USB

</div>

---

<div align="left">

## 🎉 FASE 2: PRIMER BOOT

</div>

### 🔄 Reiniciar sistema

```bash
reboot
```

<div align="left">

### 🔴 **QUITA EL USB**

</div>

### 🔐 Login

<table>
<tr>
<td width="50%">

**👤 Usuario:** Tu usuario (NO root)

</td>
<td width="50%">

**🔑 Contraseña:** La que configuraste

</td>
</tr>
</table>

> Arrancará en terminal (sin GUI todavía)

---

<div align="left">

## 🔧 FASE 3: POST-INSTALACIÓN MANUAL

</div>

### 3.1 📦 Actualizar sistema

```bash
sudo pacman -Syu
```

### 3.2 🖥️ Instalar SDDM (login gráfico)

<div align="left">

> ⚠️ **IMPORTANTE:** archinstall NO instala SDDM con perfil minimal

</div>

```bash
# Instalar
sudo pacman -S sddm sddm-kcm

# Activar
sudo systemctl enable sddm

# Iniciar (o reinicia después)
sudo systemctl start sddm
```

### 3.3 ✨ Paquetes esenciales de Plasma

<details>
<summary><b>📦 ¿Qué instala archinstall con KDE Minimal?</b></summary>

<br>

<table>
<tr>
<th>✅ Instalado</th>
<th>❌ NO instalado</th>
</tr>
<tr>
<td>

- `plasma-desktop`
- Drivers GPU
- `pipewire`
- `NetworkManager`

</td>
<td>

- Applets (volumen, red)
- Apps (dolphin, kate, etc.)
- Fuentes
- Codecs
- **Todo lo demás** 👇

</td>
</tr>
</table>

</details>

<br>

**Instalar paquetes personalizados:**

```bash
sudo pacman -S gwenview kate okular ark kalk systemsettings \
  plasma-pa breeze breeze-gtk plasma-systemmonitor \
  plasma-browser-integration oxygen oxygen-sounds kitty kdenlive \
  ocean-sound-theme ffmpegthumbs kde-system-meta plasma-welcome \
  plasma-nm xdg-desktop-portal-kde powerdevil
```

<details>
<summary><b>📝 ¿Qué hace cada paquete?</b></summary>

<br>

<table>
<tr>
<th width="40%">📦 Paquete</th>
<th width="60%">🔧 Función</th>
</tr>
<tr>
<td><code>gwenview</code></td>
<td>Visor de imágenes</td>
</tr>
<tr>
<td><code>kate</code></td>
<td>Editor de texto</td>
</tr>
<tr>
<td><code>okular</code></td>
<td>Visor de PDFs</td>
</tr>
<tr>
<td><code>ark</code></td>
<td>Compresor de archivos</td>
</tr>
<tr>
<td><code>kalk</code></td>
<td>Calculadora</td>
</tr>
<tr>
<td><code>systemsettings</code></td>
<td>Configuración del sistema</td>
</tr>
<tr style="background-color:#fff3cd;">
<td><code>plasma-pa</code></td>
<td><b>⚠️ Applet volumen (CRÍTICO)</b></td>
</tr>
<tr>
<td><code>breeze</code> / <code>breeze-gtk</code></td>
<td>Temas visuales</td>
</tr>
<tr>
<td><code>plasma-systemmonitor</code></td>
<td>Monitor de recursos</td>
</tr>
<tr>
<td><code>plasma-browser-integration</code></td>
<td>Integración navegador</td>
</tr>
<tr>
<td><code>oxygen</code> / <code>oxygen-sounds</code></td>
<td>Temas adicionales</td>
</tr>
<tr>
<td><code>kitty</code></td>
<td>Terminal GPU-accelerated</td>
</tr>
<tr>
<td><code>kdenlive</code></td>
<td>Editor de vídeo</td>
</tr>
<tr>
<td><code>ocean-sound-theme</code></td>
<td>Tema de sonidos</td>
</tr>
<tr>
<td><code>ffmpegthumbs</code></td>
<td>Miniaturas de vídeo</td>
</tr>
<tr>
<td><code>kde-system-meta</code></td>
<td>Dolphin, partitionmanager, etc.</td>
</tr>
<tr>
<td><code>plasma-welcome</code></td>
<td>Pantalla de bienvenida</td>
</tr>
<tr style="background-color:#fff3cd;">
<td><code>plasma-nm</code></td>
<td><b>⚠️ Applet red (CRÍTICO)</b></td>
</tr>
<tr>
<td><code>xdg-desktop-portal-kde</code></td>
<td>Integración Flatpak</td>
</tr>
<tr>
<td><code>powerdevil</code></td>
<td>Gestión de energía</td>
</tr>
</table>

</details>

### 3.4 🔤 Fuentes básicas

```bash
sudo pacman -S ttf-dejavu ttf-liberation noto-fonts noto-fonts-emoji
```

### 3.5 🎬 Codecs multimedia

```bash
sudo pacman -S vlc ffmpeg gst-plugins-good gst-plugins-bad gst-plugins-ugly gst-libav
```
### 3.6 🔊 Configurar audio con Pipewire

<table>
<tr>
<th>📦 Paquetes necesarios</th>
<th>🔧 Servicios a activar</th>
</tr>
<tr>
<td>

```bash
sudo pacman -S pipewire \
   wireplumber \
   pipewire-pulse \
   pipewire-alsa
```

</td>
<td>

```bash
sudo systemctl enable --now pipewire.service
sudo systemctl enable --now wireplumber.service 
sudo systemctl enable --now pipewire-pulse.service
```

</td>
</tr>
</table>

> ⚠️ **IMPORTANTE**: Activa los servicios uno por uno para evitar errores de dependencias

<details>
<summary><b>ℹ️ ¿Qué hace cada componente?</b></summary>

- `pipewire`: Servidor de audio moderno
- `wireplumber`: Gestor de sesiones
- `pipewire-pulse`: Compatibilidad PulseAudio
- `pipewire-alsa`: Compatibilidad ALSA

</details>

```

### 3.7 🚀 Iniciar Plasma

```bash
sudo systemctl start sddm
# O reinicia: reboot
```

<div align="center">

## ✅ ¡Deberías ver el login gráfico de SDDM!

<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/d/d4/Simple-desktop-display-manager.jpg/250px-Simple-desktop-display-manager.jpg" width="350px" height="250px"/>

</div>

---

<div align="left">

## ⚡ FASE 4 (OPCIONAL): OPTIMIZACIONES

### 📖 [Ver guía completa de optimizaciones →](./docs/optimizaciones.md)

</div>

<table>
<tr>
<th>⚡ Optimización</th>
<th>💾 Ahorro</th>
<th>⭐ Dificultad</th>
</tr>
<tr>
<td>💾 TRIM para SSD</td>
<td>Mantiene rendimiento</td>
<td>⭐ Fácil</td>
</tr>
<tr>
<td>🗂️ Desactivar Baloo</td>
<td>~200MB RAM</td>
<td>⭐ Fácil</td>
</tr>
<tr>
<td>🔄 Zram</td>
<td>+1-2GB swap</td>
<td>⭐⭐ Medio</td>
</tr>
<tr>
<td>📉 Reducir swappiness</td>
<td>Menos I/O disco</td>
<td>⭐ Fácil</td>
</tr>
</table>

---

<div align="left">

## 📦 FASE 5 (OPCIONAL): EXTRAS

### 📖 [Ver guía completa de extras →](./docs/extras.md)

</div>

<table>
<tr>
<th>📦 Categoría</th>
<th>🔧 Herramientas</th>
</tr>
<tr>
<td>📦 Paquetes</td>
<td>Flatpak, yay (AUR)</td>
</tr>
<tr>
<td>🖥️ Hardware</td>
<td>Bluetooth, impresoras, laptop</td>
</tr>
<tr>
<td>🎮 Gaming</td>
<td>Steam, Lutris, GameMode</td>
</tr>
<tr>
<td>💻 Desarrollo</td>
<td>VS Code, lenguajes, Docker</td>
</tr>
<tr>
<td>🎨 Multimedia</td>
<td>GIMP, Audacity, OBS</td>
</tr>
</table>

---

<div align="left">

## ⚠️ TROUBLESHOOTING COMÚN

</div>

<details>
<summary><b>📶 WiFi no conecta</b></summary>

<br>

```bash
sudo systemctl restart NetworkManager

# O con iwctl
iwctl
[iwd]# station wlan0 connect "NOMBRE_RED"
[iwd]# exit
```

</details>

<details>
<summary><b>🔊 Audio no funciona</b></summary>

<br>

```bash
# Verificar
systemctl --user status pipewire pipewire-pulse

# Reiniciar
systemctl --user restart pipewire pipewire-pulse wireplumber

# GUI de control
sudo pacman -S pavucontrol
pavucontrol
```

</details>

<details>
<summary><b>⬛ Pantalla negra después de login</b></summary>

<br>

```bash
# Ctrl+Alt+F2 (cambiar a tty2)
# Login como usuario

rm -rf ~/.cache
rm -rf ~/.config/plasma*

sudo systemctl restart sddm
```

</details>

<details>
<summary><b>💿 GRUB no detecta dual boot</b></summary>

<br>

```bash
sudo pacman -S os-prober
sudo os-prober
sudo grub-mkconfig -o /boot/grub/grub.cfg
```

</details>

<details>
<summary><b>💡 Brillo pantalla (laptop)</b></summary>

<br>

```bash
sudo pacman -S brightnessctl
brightnessctl set 50%
```

</details>

<details>
<summary><b>📜 Ver logs de errores</b></summary>

<br>

```bash
journalctl -p 3 -b                # Errores recientes
journalctl -u sddm -b             # Logs SDDM
journalctl -u NetworkManager -b   # Logs red
```

</details>

---

<div align="left">

## 🧹 MANTENIMIENTO REGULAR

</div>

### 🔄 Actualizar

```bash
sudo pacman -Syu    # Repos oficiales
yay -Syu            # Con AUR (si instalaste yay)
```

### 🗑️ Limpiar huérfanos

```bash
pacman -Qdtq                        # Ver huérfanos
sudo pacman -Rns $(pacman -Qdtq)    # Eliminar
```

### 💾 Limpiar caché

```bash
sudo pacman -Sc     # Mantener última versión
sudo pacman -Scc    # LIMPIAR TODO (⚠️ cuidado)
```

---

<div align="left">

## 📊 RESUMEN DE PAQUETES

</div>

### 🤖 Instalados por archinstall

<table>
<tr>
<td>

- ✅ `plasma-desktop` - Escritorio base
- ✅ Drivers GPU
- ✅ `pipewire` - Audio
- ✅ `NetworkManager` - Red

</td>
</tr>
</table>

### ✅ Post-instalación manual (FASE 3)

```
SDDM (2): sddm sddm-kcm

Plasma (21): gwenview kate okular ark kalk systemsettings
plasma-pa breeze breeze-gtk plasma-systemmonitor plasma-browser-integration
oxygen oxygen-sounds kitty kdenlive ocean-sound-theme ffmpegthumbs
kde-system-meta plasma-welcome plasma-nm xdg-desktop-portal-kde powerdevil

Fuentes (4): ttf-dejavu ttf-liberation noto-fonts noto-fonts-emoji

Codecs (6): vlc ffmpeg gst-plugins-good gst-plugins-bad gst-plugins-ugly gst-libav
```

---

<div align="left">

## ✅ CHECKLIST

</div>

<table width="100%">
<tr>
<th width="33%">📋 Instalación base</th>
<th width="33%">⚙️ Post-instalación</th>
<th width="34%">🎨 Opcional</th>
</tr>
<tr>
<td valign="top">

- [ ] ISO + SHA256
- [ ] USB Ventoy
- [ ] BIOS (UEFI)
- [ ] Conectar red
- [ ] `archinstall`
- [ ] KDE Minimal
- [ ] Reboot

</td>
<td valign="top">

- [ ] `pacman -Syu`
- [ ] SDDM
- [ ] Plasma (21)
- [ ] Fuentes (4)
- [ ] Codecs (6)
- [ ] Iniciar SDDM

</td>
<td valign="top">

- [ ] [Optimizaciones](./docs/optimizaciones.md)
- [ ] [Flatpak](./docs/extras.md#-flatpak)
- [ ] [yay](./docs/extras.md#-aur-helper-yay)
- [ ] Bluetooth
- [ ] Gaming

</td>
</tr>
</table>

---

<div align="center">

## 🎉 ¡SISTEMA LISTO PARA USAR!

<img src="https://raw.githubusercontent.com/catppuccin/catppuccin/main/assets/footers/gray0_ctp_on_line.svg" width="600px"/>

### 💬 ¿Problemas o sugerencias?

<p>
  <a href="https://github.com/TU_USUARIO/REPO/issues">
    <img src="https://img.shields.io/badge/Reportar_Issue-red?style=for-the-badge&logo=github" alt="Issues"/>
  </a>
  <a href="https://github.com/TU_USUARIO/REPO/pulls">
    <img src="https://img.shields.io/badge/Contribuir-green?style=for-the-badge&logo=github" alt="Pull Requests"/>
  </a>
</p>

---

**Hecho con ❤️ por la comunidad de Arch Linux**

<img src="https://img.shields.io/badge/License-MIT-green?style=for-the-badge" alt="License"/>

</div>
