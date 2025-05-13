Edificio Gubernamental:
Vtp domain: VTPserver
Password:uaxlab


Edificios:
Vtp domain: Ciudad
Password: uaxlab



# Paso 1: Diseño y Modelado de la Arquitectura de Comunicación

## Repaso de modelos OSI y TCP/IP

### Modelo OSI

El **modelo OSI** consta de **siete capas** que estructuran el proceso de comunicación de datos entre sistemas, dividiendo funciones específicas para garantizar una comunicación clara, ordenada y estandarizada:

1. **Capa Física**  
   Responsable de la **transmisión de bits** a través de medios físicos como cables trenzados o fibra óptica. Define estándares mecánicos, eléctricos y ópticos como tensiones, tiempos de señal y tipos de conectores.  
   *Ejemplos*: Cables de red, conectores, tarjetas de red.

2. **Capa de Enlace de Datos**  
   Convierte el medio físico en una línea de comunicación confiable mediante la **detección y corrección de errores**, organizando los datos en tramas. Se divide en subcapas de acceso al medio y control de flujo.  
   *Ejemplos*: Switches, adaptadores de red, Ethernet.

3. **Capa de Red**  
   Encargada del **enrutamiento** de datos entre redes, gestionando direcciones IP, tablas de enrutamiento, congestión y calidad del servicio. Puede usar rutado estático o dinámico.  
   *Ejemplos*: Routers, direcciones IP.

4. **Capa de Transporte**  
   Ofrece **comunicación extremo a extremo confiable**, segmentando datos y asegurando entrega ordenada. Puede operar con protocolos orientados a conexión (TCP) o sin conexión (UDP).  
   *Ejemplos*: TCP, UDP.

5. **Capa de Sesión**  
   Establece, administra y finaliza sesiones entre aplicaciones, proporcionando sincronización y control de diálogos entre sistemas.

6. **Capa de Presentación**  
   Traduce y transforma los datos, asegurando que los sistemas con diferentes formatos puedan **interpretar la información correctamente**. Maneja compresión y cifrado.

7. **Capa de Aplicación**  
   Interactúa directamente con el **usuario final**, proporcionando servicios como transferencia de archivos, correo electrónico o navegación web.  
   *Ejemplos*: HTTP, FTP, SMTP.

---

### Modelo TCP/IP

El **modelo TCP/IP**, base de Internet, es un modelo más práctico y consta de **cuatro capas**, integrando funciones del modelo OSI para facilitar su implementación en sistemas reales:

1. **Capa de Acceso a la Red**  
   Equivalente a las capas Física y de Enlace del OSI. Maneja el hardware, controladores y protocolos de acceso al medio físico.

2. **Capa de Internet**  
   Similar a la Capa de Red del OSI. Administra direcciones IP, fragmentación y enrutamiento de paquetes entre redes.

3. **Capa de Transporte**  
   Igual que en OSI, se encarga del control de flujo, confiabilidad y segmentación de datos. Utiliza **TCP** (orientado a conexión) o **UDP** (sin conexión).

4. **Capa de Aplicación**  
   Agrupa las capas de Aplicación, Presentación y Sesión del OSI. Proporciona servicios de red al usuario y aplicaciones.  
   *Ejemplos*: HTTP, FTP, DNS.



 ***Comparación entre el Modelo OSI y el Modelo TCP/IP***

| **Capa**   | **Modelo OSI**             | **Modelo TCP/IP**              |
|-----------|-----------------------------|-------------------------------|
| Capa 1    | Física                      | Acceso a la Red               |
| Capa 2    | Enlace de Datos             | Acceso a la Red               |
| Capa 3    | Red                         | Internet                      |
| Capa 4    | Transporte                  | Transporte                    |
| Capa 5    | Sesión                      | Aplicación (combinada)        |
| Capa 6    | Presentación                | Aplicación (combinada)        |
| Capa 7    | Aplicación                  | Aplicación (combinada)        |


## Diseño Lógico y Segmentación: 

Zonas Genéricas, Transporte e Internet
1. Zona Genérica – Ciudad Inteligente
Descripción: Esta zona representa distintos servicios distribuidos en la ciudad: control de acceso, vigilancia IoT, sensores ambientales, multimedia, salud, infraestructura crítica y comunicación ciudadana.

Segmentación: Está dividida por áreas funcionales (seguridad, monitoreo, salud, etc.) mediante VLANs, con switches y routers que gestionan el tráfico internamente.

Transporte: El tráfico se distribuye a través de switches de acceso y un router central de la ciudad que actúa como punto de salida. La conectividad se realiza mediante enlaces Ethernet.

Internet: El acceso a Internet se canaliza a través de un servidor de borde en la DMZ de la ciudad. Hay presencia de servidores DNS, DHCP, y HTTP para la gestión interna y externa.

2. Zona Genérica – Edificio Gubernamental
Descripción: Esta zona simula una oficina administrativa conectada a una red institucional mayor. Contiene equipos de trabajo, servidores y sistemas internos.

Segmentación: Se agrupa por funciones administrativas, DMZ y servidores. Cada sección está conectada mediante switches y estructurada en VLANs.

Transporte: El transporte de datos se realiza por medio de enlaces de cobre, incluyendo conexiones cruzadas entre switches y routers para mejorar la redundancia y eficiencia.

Internet: Esta red se conecta a la red de ciudad mediante un enlace serial WAN, por donde accede a los servicios de Internet y servidores externos, usando NAT si es necesario.

3. Conectividad entre Zonas
Ambas redes están interconectadas mediante un enlace serial punto a punto, que permite el enrutamiento entre los dominios y centraliza el acceso a servicios comunes como Internet o DNS.


Tipos de Enlace Utilizados
El diseño de red implementa diferentes tipos de enlaces físicos adaptados a las necesidades de cada zona, considerando la velocidad, confiabilidad y tipo de dispositivo:

1. Enlaces de Cobre (Ethernet)
Se utiliza cableado UTP de cobre (categoría 5e o superior) para la mayoría de las conexiones locales.

Se implementan enlaces Fast Ethernet (100 Mbps) y Gigabit Ethernet (1000 Mbps), según la capacidad de los equipos involucrados.

Todas las conexiones están configuradas en modo full-duplex, lo que permite transmisión y recepción simultánea sin colisiones, gracias a la eliminación del dominio compartido de colisión.

Esto mejora la eficiencia y el rendimiento en las comunicaciones entre PCs, switches, routers y servidores.

2. Cables Directos y Cruzados
Se usan cables cruzados para conexiones entre dispositivos del mismo tipo (por ejemplo, switch-switch o router-router) cuando el dispositivo no soporta auto-MDI/MDIX.

Se utilizan cables directos para conexiones entre dispositivos diferentes (por ejemplo, PC a switch, router a switch).


## Recuento de Dispositivos por Zona

### Edificio Gubernamental 

| Tipo de Dispositivo         | Cantidad Aproximada | Observaciones                                      |
|----------------------------|---------------------|---------------------------------------------------|
| Router                     | 1                   | Con enlace serial hacia la red de la ciudad       |
| Switch Multicapa           | 1                   | Actúa como núcleo de distribución                 |
| Switches de acceso         | 5                   | Conectan VLANs de PCs, voz, servicios             |
| Servidores                 | 4                   | DHCP, DNS, HTTP, EMAIL (zona de servicios)        |
| PCs                        | 12+                 | Distribuidos en diferentes áreas funcionales      |
| Teléfonos IP               | 6                   | Integrados en la red de voz IP                    |
| Dispositivos IoT           | Varios              | Cámaras, sensores, control de acceso              |
| Otros                      | Varios              | MCU, altavoces, lectores de tarjetas, tablets     |

---

### Ciudad Inteligente 

| Tipo de Dispositivo         | Cantidad Aproximada | Observaciones                                      |
|----------------------------|---------------------|---------------------------------------------------|
| Router                     | 1                   | Con enlace serial al edificio gubernamental       |
| Switches                   | 4                   | Segmentación por zonas: seguridad, DMZ, etc.      |
| Servidores                 | 2                   | DHCP, DNS y servidor de borde en DMZ              |
| PCs                        | 3                   | Estaciones de control                             |
| Cámaras y sensores         | Varios              | Seguridad pública y vigilancia urbana             |
| Dispositivos IoT/Energía   | Varios              | Panel solar, batería, sensores ambientales        |
| Sistema de acceso          | 1                   | Puerta con lector RFID y cerradura electrónica    |
| Otros                      | Varios              | Megáfono Bluetooth, altavoces, lectores RFID      |

Se utiliza la fórmula de Shannon:  

$$Donde: C = B * log_2(1+SNR)$$  

Ancho de banda (B)  

SNR: relación señal a ruido determinada.   
La relación señal a ruido se mide en dB en un ancho de banda es:    

$$𝑆𝑁𝑅 = 10 𝑙𝑜𝑔_{10}(𝑆𝑁𝑅) = 10^{\frac{SNR}{10}} [dB]$$  

1. **Fa/Trenzado de 250Mb**  
    Cable de cobre categoría 6 con ancho de banda de 250 MHz. 

    $$C = 2,5 * 10^8 * log_2(1+1000) = 2,5 * 10^8 * log_2(1001) = 2,5 * 10^8 * 9.967 = 2.49 * 10^9bps = 2.49 Gbps$$

   *Este tipo de cable proporciona conexiones repidas entre switches-ordenadores *


   2. **Acces-point/Inalámbrico**
   Enlaces inalambricos de wifi en cada access-point.


   $$C = B \cdot \log_2(1 + S/N) = 20 \times 10^6 \cdot \log_2(101) \approx 20 \times 10^6 \cdot 6.658 = 133.16 \text{ Mbps}$$


   ### Enlace entre Switches – Cable de Cobre Gigabit Ethernet

Se utiliza **cableado de cobre** con soporte para **Gigabit Ethernet (1 Gbps)** en las conexiones troncales entre switches y hacia los routers. Estos enlaces permiten un transporte de datos de alta velocidad en la infraestructura interna de la red.

- **Tipo de cable:** Cobre UTP categoría 5e/6
- **Ancho de banda estimado:** 1 GHz
- **Cálculo teórico de capacidad** utilizando la fórmula de capacidad de canal de Shannon:

\[
C = B \cdot \log_2(1 + SNR) = 1 \cdot 10^9 \cdot \log_2(1001) \approx 1 \cdot 10^9 \cdot 9.97 = 9.97 \cdot 10^9 \text{ bps}
\]

- **Resultado:** ≈ **9.97 Gbps** teóricos en condiciones ideales

> Este tipo de enlace proporciona un **canal de alta capacidad y baja latencia**, ideal para el intercambio de grandes volúmenes de datos entre switches, así como entre switches y routers dentro del núcleo de red. La





