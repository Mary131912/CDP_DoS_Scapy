# 🚨 CDP DoS Attack - Scapy

**Ataque de Denegación de Servicio contra el Protocolo CDP (Cisco Discovery Protocol)**

---

## 📋 Información General

- **Autor:** Mariana Doñe Lara
- **Matrícula:** 20241200
- **Objetivo:** Demostración académica de vulnerabilidades en CDP
- **Plataforma:** PNETLab
- **Entorno:** Controlado y con fines educativos

---

## 📚 Descripción

Este repositorio contiene un script desarrollado en **Python** utilizando la librería **Scapy**, cuyo objetivo es realizar un ataque de Denegación de Servicio (DoS) al plano de control de un switch Cisco mediante la inyección masiva de paquetes CDP falsos.

El ataque explota el protocolo **Cisco Discovery Protocol (CDP)**, el cual opera en **Capa 2** y permite a los dispositivos Cisco intercambiar información de forma automática.

> ⚠️ **Advertencia Legal:** Este código es solo para fines educativos en entornos controlados autorizados.

---

## 🎯 Objetivo del Script

El objetivo del script es:

- ✅ Inundar el switch con paquetes CDP falsificados
- ✅ Generar múltiples vecinos CDP inexistentes
- ✅ Saturar el plano de control del switch
- ✅ Demostrar la falta de autenticación del protocolo CDP
- ✅ Realizar prácticas de seguridad en redes y pentesting interno

---

## 🏗️ Topología de Red
