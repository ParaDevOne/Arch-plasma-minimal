<div align="center">

# ⚡ OPTIMIZACIONES DE RENDIMIENTO

### Mejoras opcionales para optimizar Arch Linux + KDE Plasma

<img src="https://img.shields.io/badge/Rendimiento-Up_to_30%25-brightgreen?style=for-the-badge" alt="Performance"/>
<img src="https://img.shields.io/badge/RAM_Ahorro-~200MB-blue?style=for-the-badge" alt="RAM"/>
<img src="https://img.shields.io/badge/Dificultad-Fácil-success?style=for-the-badge" alt="Easy"/>

</div>

---

## 📋 CONTENIDO

<table>
<tr>
<td width="50%" valign="top">

**💾 Rendimiento**
- [TRIM para SSD](#-trim-para-ssd)
- [Zram (swap comprimido)](#-zram-swap-comprimido)
- [Reducir swappiness](#-reducir-swappiness)

</td>
<td width="50%" valign="top">

**🗂️ RAM & Recursos**
- [Desactivar Baloo](#️-desactivar-indexación-baloo)
- [Verificar mejoras](#-verificar-mejoras)
- [Resumen](#-resumen-de-optimizaciones)

</td>
</tr>
</table>

---

<div align="center">

## 💾 TRIM PARA SSD

<img src="https://img.shields.io/badge/Ahorro-Mantiene_Rendimiento-success?style=flat-square" alt="Ahorro"/>
<img src="https://img.shields.io/badge/Dificultad-⭐_Fácil-blue?style=flat-square" alt="Fácil"/>

</div>

### 📖 ¿Qué es TRIM?

<table>
<tr>
<td width="60%">

TRIM es un comando que informa al SSD qué bloques de datos ya no están en uso. 

**Beneficios:**
- ✅ Mantiene rendimiento de escritura
- ✅ Prolonga vida útil del SSD
- ✅ Velocidad constante

</td>
<td width="40%">

```bash
# Verificar soporte
sudo hdparm -I /dev/sda | grep TRIM
```

</td>
</tr>
</table>

### 🔧 Instalación

```bash
# Activar servicio TRIM semanal
sudo systemctl enable fstrim.timer

# Verificar estado
systemctl status fstrim.timer

# Ejecutar TRIM manualmente
sudo fstrim -v /
```

<details>
<summary><b>📊 Ver estadísticas de TRIM</b></summary>

<br>

```bash
# Ver última ejecución
systemctl status fstrim.timer

# Logs de ejecución
journalctl -u fstrim
```

</details>

---

<div align="center">

## 🗂️ DESACTIVAR INDEXACIÓN BALOO

<img src="https://img.shields.io/badge/Ahorro-~200_300MB_RAM-success?style=flat-square" alt="Ahorro RAM"/>
<img src="https://img.shields.io/badge/Dificultad-⭐_Fácil-blue?style=flat-square" alt="Fácil"/>

</div>

### 📖 ¿Qué es Baloo?

<table>
<tr>
<td>

Baloo es el **indexador de archivos de KDE**. Consume recursos para indexar todos tus archivos y permitir búsquedas rápidas.

</td>
</tr>
</table>

### ⚖️ ¿Cuándo desactivarlo?

<table>
<tr>
<th width="50%">✅ Desactivar si...</th>
<th width="50%">❌ Mantener si...</th>
</tr>
<tr>
<td>

- Tienes poca RAM (<8GB)
- No usas búsqueda frecuente
- Quieres máximo rendimiento
- Tienes muchos archivos

</td>
<td>

- Usas búsqueda de archivos diariamente
- Tienes RAM suficiente (16GB+)
- Trabajas con muchos documentos
- Necesitas búsquedas instantáneas

</td>
</tr>
</table>

### 🔧 Desactivar Baloo

```bash
# Desactivar indexación
systemctl --user mask baloo_file

# Verificar estado (debe mostrar "masked")
systemctl --user status baloo_file

# Limpiar índice existente (opcional)
rm -rf ~/.local/share/baloo
```

### ♻️ Reactivar Baloo

```bash
systemctl --user unmask baloo_file
systemctl --user start baloo_file
```

<details>
<summary><b>⚙️ Alternativa: Configurar carpetas excluidas</b></summary>

<br>

**Sin desactivar completamente:**

1. Abrir **System Settings**
2. **Search** → **File Search**
3. **Folder specific configuration**
4. Excluir carpetas pesadas (Downloads, Videos, etc.)

</details>

---

<div align="center">

## 💾 ZRAM (SWAP COMPRIMIDO)

<img src="https://img.shields.io/badge/Ahorro-+1_2GB_Swap-success?style=flat-square" alt="Ahorro"/>
<img src="https://img.shields.io/badge/Dificultad-⭐⭐_Medio-orange?style=flat-square" alt="Medio"/>

</div>

### 📖 ¿Qué es Zram?

<table>
<tr>
<td width="60%">

Zram crea un **dispositivo de swap comprimido en RAM**.

**Ventajas:**
- 🚀 ~2-3x ratio de compresión
- ⚡ Mucho más rápido que swap en disco
- 💾 Ideal para 4-16GB RAM

</td>
<td width="40%">

```bash
# Ver uso
zramctl
free -h
```

</td>
</tr>
</table>

### 🔧 Instalación

```bash
# Instalar zram-generator
sudo pacman -S zram-generator

# Crear configuración
sudo tee /etc/systemd/zram-generator.conf <<EOF
[zram0]
zram-size = ram / 2
compression-algorithm = zstd
EOF

# Recargar systemd
sudo systemctl daemon-reload

# Iniciar zram
sudo systemctl start systemd-zram-setup@zram0.service

# Verificar
zramctl
swapon --show
```

### ⚙️ Configuración avanzada

<details>
<summary><b>💻 Para 8GB+ RAM (menos agresivo)</b></summary>

```ini
[zram0]
zram-size = ram / 4
compression-algorithm = zstd
```

</details>

<details>
<summary><b>📱 Para 4GB RAM (más agresivo)</b></summary>

```ini
[zram0]
zram-size = ram
compression-algorithm = zstd
```

</details>

### 📊 Verificar funcionamiento

```bash
# Uso actual
free -h

# Estadísticas detalladas
cat /sys/block/zram0/mm_stat

# Ratio de compresión
cat /sys/block/zram0/comp_algorithm
```

---

<div align="center">

## 📉 REDUCIR SWAPPINESS

<img src="https://img.shields.io/badge/Ahorro-Menos_I/O_Disco-success?style=flat-square" alt="Ahorro"/>
<img src="https://img.shields.io/badge/Dificultad-⭐_Fácil-blue?style=flat-square" alt="Fácil"/>

</div>

### 📖 ¿Qué es swappiness?

<table>
<tr>
<td>

Swappiness controla **cuándo el sistema usa swap**. 

**Valor por defecto:** 60 (usa swap frecuentemente)

</td>
</tr>
</table>

### 🎯 Valores recomendados

<table>
<tr>
<th>💻 Uso</th>
<th>🔢 Swappiness</th>
<th>📝 Razón</th>
</tr>
<tr>
<td>Desktop/Laptop</td>
<td><code>10</code></td>
<td>Menos uso de disco, más rápido</td>
</tr>
<tr>
<td>Servidor</td>
<td><code>60</code></td>
<td>Balance entre RAM y swap</td>
</tr>
<tr>
<td>Con zram</td>
<td><code>100</code></td>
<td>Prioriza swap comprimido en RAM</td>
</tr>
</table>

### 🔧 Configuración

```bash
# Configuración temporal (hasta reinicio)
sudo sysctl vm.swappiness=10

# Configuración permanente
echo "vm.swappiness=10" | sudo tee /etc/sysctl.d/99-swappiness.conf

# Aplicar cambios
sudo sysctl -p /etc/sysctl.d/99-swappiness.conf

# Verificar
cat /proc/sys/vm/swappiness
```

---

<div align="center">

## 📊 VERIFICAR MEJORAS

</div>

### ⏱️ Tiempo de arranque

```bash
# Tiempo total de boot
systemd-analyze

# Servicios más lentos
systemd-analyze blame

# Cadena crítica
systemd-analyze critical-chain
```

### 💾 Uso de RAM

<table>
<tr>
<td width="50%">

**Antes de optimizar:**

```bash
free -h
# Usar como referencia
```

</td>
<td width="50%">

**Después de optimizar:**

```bash
free -h
# Comparar diferencias
```

</td>
</tr>
</table>

### 💿 Uso de disco (I/O)

```bash
# Monitor en tiempo real
sudo iotop

# Estadísticas
iostat -x 1
```

---

<div align="center">

## 🎯 RESUMEN DE OPTIMIZACIONES

</div>

<table>
<tr>
<th>⚡ Optimización</th>
<th>💾 Ahorro estimado</th>
<th>⭐ Dificultad</th>
<th>⏱️ Tiempo</th>
</tr>
<tr>
<td>💾 TRIM (SSD)</td>
<td>Mantiene rendimiento</td>
<td>⭐ Fácil</td>
<td>1 min</td>
</tr>
<tr>
<td>🗂️ Baloo OFF</td>
<td>~200MB RAM</td>
<td>⭐ Fácil</td>
<td>1 min</td>
</tr>
<tr>
<td>💾 Zram</td>
<td>+1-2GB swap</td>
<td>⭐⭐ Medio</td>
<td>3 min</td>
</tr>
<tr>
<td>📉 Swappiness=10</td>
<td>Menos I/O disco</td>
<td>⭐ Fácil</td>
<td>1 min</td>
</tr>
</table>

### 💡 Recomendación por perfil

<details>
<summary><b>🖥️ Desktop (16GB+ RAM)</b></summary>

<br>

```bash
# TRIM + Swappiness
sudo systemctl enable fstrim.timer
echo "vm.swappiness=10" | sudo tee /etc/sysctl.d/99-swappiness.conf
```

</details>

<details>
<summary><b>💻 Laptop (8GB RAM)</b></summary>

<br>

```bash
# TODO: TRIM + Baloo OFF + Zram + Swappiness
sudo systemctl enable fstrim.timer
systemctl --user mask baloo_file
# Instalar zram (ver arriba)
echo "vm.swappiness=10" | sudo tee /etc/sysctl.d/99-swappiness.conf
```

</details>

<details>
<summary><b>📱 Low-end (4GB RAM)</b></summary>

<br>

```bash
# TODO + zram agresivo
sudo systemctl enable fstrim.timer
systemctl --user mask baloo_file
# zram con zram-size = ram (ver arriba)
echo "vm.swappiness=100" | sudo tee /etc/sysctl.d/99-swappiness.conf
```

</details>

<div align="center">

### [← Volver al README](../README.md)

<img src="https://raw.githubusercontent.com/catppuccin/catppuccin/main/assets/footers/gray0_ctp_on_line.svg" width="600px"/>

</div>
