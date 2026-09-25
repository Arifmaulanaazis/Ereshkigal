<div align="center">

<img src="assets/logo.png" width="96" height="96" alt="Ereshkigal">

# Ereshkigal Project

**Grabación en un clic del firmware de pruebas de seguridad Wi-Fi Ereshkigal RTL8720DN (BW16).**

Sin Arduino IDE. Sin código fuente. Sin línea de comandos. Solo esta carpeta.

[English](README.md) · [Bahasa Indonesia](README.id.md) · **Español** · [Français](README.fr.md) · [Deutsch](README.de.md) · [中文](README.zh.md)

![versión](https://img.shields.io/badge/versión-2.0.0-6c4cf1)
![plataforma](https://img.shields.io/badge/plataforma-Windows%2010%2F11-2fa565)
![placa](https://img.shields.io/badge/placa-RTL8720DN%20(BW16)-14161d)
![idiomas](https://img.shields.io/badge/idiomas%20UI-6-e0870b)

</div>

> [!WARNING]
> **Aviso legal y de seguridad léelo antes de usar.**
> Ereshkigal es una herramienta de **pruebas de seguridad** Wi-Fi. Úsala **solo**:
> - en redes y dispositivos **de tu propiedad**, o con **permiso explícito por escrito** para probarlos;
> - dentro de un **entorno de laboratorio / pruebas controlado** que hayas preparado.
>
> **No** la uses contra redes, dispositivos o personas que no estés autorizado a
> probar. Interceptar o interrumpir redes inalámbricas sin autorización es
> **ilegal en la mayoría de los países** y puede acarrear **cargos penales**. Este
> proyecto es solo para educación, investigación, CTFs y pruebas de penetración
> autorizadas. **Tú eres el único responsable de su uso.**

---

<p align="center">
  <img src="assets/screenshot-flasher.png" width="330" alt="Ereshkigal Project (Windows)">
  &nbsp;&nbsp;
  <img src="assets/screenshot-device.png" width="300" alt="Interfaz web del dispositivo Ereshkigal">
</p>
<p align="center"><sub>Izquierda: el flasher en Windows. Derecha: el panel web integrado del dispositivo tras grabarlo.</sub></p>

## Contenido

| Archivo | Qué es |
|---------|--------|
| **`EreshkigalFlasher.exe`** | La app de grabación (Windows, autónoma). |
| **`Ereshkigal.efw`** | El firmware, en el formato protegido de Ereshkigal. |

Distribuye ambos archivos juntos. La app es una pequeña ventana nativa en
**English, Bahasa Indonesia, Español, Français, Deutsch y 中文** cámbialo en el
selector de arriba a la derecha.

## Requisitos

- **Windows 10 u 11.** Usa el **runtime WebView2** integrado (incluido en Windows
  11 y Windows 10 actual; si falta, instala una vez el *Microsoft Edge WebView2
  Runtime* gratuito).
- Una placa **RTL8720DN / BW16** y un cable USB de **datos**.
- El **driver USB-serie** de la placa (la mayoría usan CH340 o CP2102) para que
  aparezca como puerto `COM`.

## Tutorial graba en 4 pasos

1. **Conecta** la placa por USB y ejecuta **`EreshkigalFlasher.exe`**.
2. `Ereshkigal.efw` ya está seleccionado. Elige el **puerto COM** de tu placa en
   la lista (pulsa actualizar si no aparece desconecta/reconecta la placa y
   actualiza; la entrada nueva es tu placa).
3. Deja **Velocidad** en `1500000`.
4. Pulsa **Grabar firmware**, espera a **Hecho** y reinicia la placa.

La mayoría entra sola en modo de grabación. **Si el registro se atasca**, haz la
secuencia de botones **Modo de descarga** en la placa:

```
   ┌── 1 ──┐      ┌── 2 ──┐      ┌── 3 ──┐
   │ BOOT  │  →   │ RESET │  →   │ BOOT  │
   │mantén │      │ pulsa │      │suelta │
   └───────┘      └───────┘      └───────┘
   mantén BOOT · pulsa RESET · suelta BOOT
```

El flasher reintenta la sincronización automáticamente (hasta 3×).

## Primer arranque tras la grabación

1. El dispositivo emite una red Wi-Fi **abierta** llamada **`Ereshkigal`**.
2. Únete y abre **http://192.168.1.1/**.
3. Completa el **asistente de configuración** una vez pon un nombre de red y una
   contraseña (8–63 caracteres). El dispositivo la guarda y se reinicia.
4. Reconéctate con tu contraseña, reabre **http://192.168.1.1/** y el panel
   completo queda desbloqueado.

## Úsalo para una comprobación WPA2 → WPA3

Ereshkigal demuestra una debilidad Wi-Fi real y común: las redes con **WPA2 sin
Protected Management Frames (PMF / 802.11w)** pueden interrumpirse con tramas de
**desautenticación** falsificadas  cualquiera cerca puede desconectar a los
clientes, y esa desconexión forzada es el primer paso de la captura del handshake
y los ataques evil-twin.

Una evaluación **autorizada** típica en tu propia red:

1. **Scan**  abre el panel, pulsa *Scan* y elige tu red objetivo.
2. **Users**  lista los dispositivos conectados.
3. **Attack**  ejecuta una prueba *deauth* y observa tus propios clientes.
4. **Detector**  dedica la radio a detectar tramas deauth en el aire.

**Interpretar el resultado**
- Los clientes **se caen** → la red es WPA/WPA2 sin PMF obligatorio y es
  vulnerable a la falsificación de tramas de gestión (denegación de servicio por
  deauth, y la cadena desconectar-y-capturar posterior).
- Los clientes **siguen conectados** → las tramas de gestión están protegidas.

**La solución  pasa a WPA3.** Cambia la red a **WPA3 (SAE)**, o como mínimo
**WPA2 con PMF en _obligatorio_** (802.11w). WPA3 exige tramas de gestión
protegidas, así que la deauth/disociación falsificada se ignora. **Repite la misma
prueba deauth después**  los clientes deberían permanecer conectados, probando que
la actualización cerró el fallo. Ese antes/después es el objetivo: usa Ereshkigal
para justificar y verificar la migración WPA2 → WPA3.

> Solo contra una red de tu propiedad o autorizada, en tu laboratorio controlado.

## Solución de problemas

| Síntoma | Solución |
|---------|----------|
| **Sin puertos COM** | Instala el driver USB-serie; usa un cable de datos (no solo de carga). |
| **"Failed to open COM…"** | Otro programa ocupa el puerto (un monitor serie, otro flasher). Ciérralo. |
| **Reintenta y falla** | Haz la secuencia del Modo de descarga mientras reintenta: mantén BOOT, pulsa RESET, suelta BOOT. |
| **Sigue fallando** | Baja la **Velocidad** a `921600` y vuelve a grabar. |

## Sobre el formato del firmware

`Ereshkigal.efw` es el firmware en el formato empaquetado propio de Ereshkigal. El
flasher lo prepara para la placa internamente no descomprimes nada ni necesitas
herramientas extra. Mantén juntos el `.exe` y el `.efw`.

---

<div align="center">
<sub>Ereshkigal por <b>Titan Digitalsoft</b> · Flasher 2.0.0 · Solo pruebas autorizadas</sub>
</div>
