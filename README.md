# Spout2 Plugin for OBS Studio (Fork / Mod)

> **Aviso de Atribución y Licencia / Attribution & License Notice:**  
> Este proyecto es una bifurcación (fork) del plugin [obs-spout2-plugin](https://github.com/off-world-live/obs-spout2-plugin) desarrollado originalmente por **Campbell Morgan** y **Off World Live Ltd (https://offworld.live)**.  
> Este software se redistribuye y modifica de acuerdo con los términos de la **GNU General Public License versión 2 (GPLv2)**.  
> *Este proyecto es un fork independiente y no está afiliado, patrocinado ni respaldado por Off World Live Ltd ni por el proyecto OBS Studio.*

---

## 🚀 Mejoras y Modificaciones de este Fork

Este fork aborda limitaciones específicas en la persistencia de fuentes y el soporte para instalaciones portátiles de OBS Studio:

1. **Persistencia de la fuente Spout seleccionada:**
   - **Problema en la versión base:** Si la fuente Spout configurada no estaba transmitiendo al iniciar OBS o al abrir las propiedades, la lista no la mostraba y OBS revertía automáticamente la selección a *"Usar la primera fuente disponible"*, sobrescribiendo la configuración.
   - **Solución:** La fuente seleccionada **se mantiene y persiste en la lista** independientemente de si el emisor está encendido o apagado en ese momento. Al encender la fuente emisora, OBS se conectará a ella de inmediato.

2. **Entrada de texto editable (`OBS_COMBO_TYPE_EDITABLE`):**
   - El selector de fuentes ahora permite escribir manualmente el nombre del emisor (por ejemplo, `CamAr Studio`) incluso antes de iniciarlo por primera vez.

3. **Botón *"Actualizar lista de fuentes"*:**
   - Se añadió un botón en el cuadro de propiedades para consultar y refrescar los emisores Spout activos al vuelo, sin tener que cerrar y reabrir el diálogo de propiedades.

4. **Compatibilidad con instalaciones portátiles (OBS 33+):**
   - Estructuración limpia y autocontenida que no depende del Registro de Windows (`HKLM\SOFTWARE\OBS Studio`) ni de rutas fijas en `C:\ProgramData`.

---

## 📋 Requisitos del Sistema

- **Sistema Operativo:** Windows 10 u 11 (64-bit).
- **OBS Studio:** Versión 33.0 o superior (64-bit).
- **Renderizador de OBS:** Direct3D 11 (renderizador predeterminado de OBS).

---

## 📦 Instalación

### Instalación en OBS portátil o en carpeta personalizada (ej. `D:\Obs-Studio`)

Para OBS Studio 33 o superior en versión descomprimida / portátil, copia los archivos en la subcarpeta `plugins\win-spout\` de tu OBS:

```text
<carpeta-de-tu-OBS>\
└── plugins\win-spout\
    ├── win-spout.dll
    ├── Spout.dll
    ├── SpoutDX.dll
    ├── SpoutLibrary.dll
    └── data\
        └── locale\
            ├── es-ES.ini
            ├── en-US.ini
            ├── pt-BR.ini
            └── zh-CN.ini
```

> **Nota:** En OBS 33, las DLLs deben ubicarse directamente en `plugins\win-spout\` (no dentro de `bin\64bit\`), lo que permite que OBS cargue el plugin y sus textos localizados de forma relativa sin generar advertencias de módulos antiguos.

---

## 🛠️ Compilación desde el Código Fuente

Requisitos para compilar:
- Visual Studio 2022 o 2026 con soporte para C++ de 64 bits.
- CMake 3.28 o superior.
- Git (con submódulos clonados: `git submodule update --init --recursive`).

Comandos para configurar y compilar:
```powershell
# Configurar el proyecto (descarga dependencias de OBS y Qt automáticamente)
cmake -B build_x64 -A x64 -DENABLE_FRONTEND_API=ON -DENABLE_QT=ON

# Compilar en modo Release
cmake --build build_x64 --config Release

# Empaquetar en carpeta de distribución
cmake --install build_x64 --prefix dist --config Release
Copy-Item "deps/Spout2/BUILD/Binaries/x64/*.dll" "dist/win-spout"
```

---

## 👥 Créditos y Agradecimientos

- **Autor original del plugin:** Campbell Morgan / [Off World Live Ltd](https://offworld.live).
- **Repositorio original de referencia:** [off-world-live/obs-spout2-plugin](https://github.com/off-world-live/obs-spout2-plugin).
- Desarrolladores de [SPOUT2](https://github.com/leadedge/Spout2) (Lynn Jarvis / leadedge) por el SDK y la arquitectura Spout.
- Al equipo y comunidad de [OBS Studio](https://obsproject.com/).
- Autores y contribuidores de [OBS-OpenVR-Input-Plugin](https://github.com/baffler/OBS-OpenVR-Input-Plugin).
- Contribuidores del proyecto base: [@shugen002](https://github.com/shugen002), [@mzlt](https://github.com/mzlt), [@terids](https://github.com/terids).

---

## 📄 Licencia y Descargo de Responsabilidad / License & Disclaimer

Este programa es software libre; puedes redistribuirlo y/o modificarlo bajo los términos de la **GNU General Public License versión 2 (GPLv2)** publicada por la Free Software Foundation. Consulta el archivo [LICENSE](./LICENSE) para más detalles.

```text
Copyright (C) 2019-2021 Off World Live Ltd
Copyright (C) 2026 Modificaciones y mejoras por juacar01

This program is free software; you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation; either version 2 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the
GNU General Public License for more details.
```
