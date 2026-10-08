<div align="center">

![KUBIX](Imagenes/02-logo.svg)

# KUBIX
### Tus juegos de siempre, con un nuevo reto!

**Juega · Comparte · Disfruta**

</div>

---

## ¿Qué es KUBIX?

KUBIX es la nueva consola de videojuegos retro y multijugador, pensada para **compartir y retarse**. Su diseño en forma de cubo pone una pantalla en cada una de sus cuatro caras laterales, para que cada lado sea una estación de juego donde todos puedan divertirsde alrededor del mismo equipo, ya sea compartiendo o poniendo a prueba sus habilidades.

Podras disfrutar de los clásicos de siempre, pero esta vez juegalos en compañía: contra un amigo en la misma pantalla o entre otras pantallas conectadas.

![Disfruta de KUBIX](Imagenes/01-consola.svg)

> **4 lados. hasta 8 jugadores. Diferentes juegos. Un espacio, ua sola consola.**

---

## Juega a full color en un espacio compacto

Cada estación tiene una pantalla a color de **64 × 64 píxeles**, con la estética clasica de píxel de los arcades clásicos. En total son **4 pantallas** independientes, Inicia las pantallas y los juegos que quieras, en el momento que qieras.

![Pantallas de KUBIX](Imagenes/04-pantallas-auxiliares.svg)

---

## Experimenta el juego de la manera que quieras

KUBIX es compatible con distintos tipos de periféricos. 

Cada estación incluye:

- **2 conectores tipo NES**, para mandos NES.
- **2 conectores PS/2**, para teclado y mouse.

Así cada jugador elige cómo jugar a su maximo nivel.

![Controles compatibles](Imagenes/03-conectividad.svg)

---

## Juegos que podras revivir

| Juego | Descripción |
|---|---|
| **Galaga** | El clásico shooter espacial. |
| **Pong** | El duelo de paletas de toda la vida. |
| **Snake** | Crece sin chocar contigo mismo. |
| **Rally** | Esquiva el tráfico y llega lo más lejos posible. |
| **Batalla naval** | Pensado para interconexión entre pantallas. |

*Y muchos más en camino...*

![Juegos de KUBIX](Imagenes/06-juegos.svg)

<!-- Debemos agregar una captura por juego y confirmar cuáles quedan en modo multijugador -->

---

## Juega a tu manera

Un cubo, cuatro estciones, infinitas posibilidades:

- **Juega solo:** disfruta tus juegos favoritos en cualquier pantalla.
- **Dos en una pantalla:** comparte la emoción con un amigo en el mismo lado del cubo.
- **Entre pantallas:** conecta las 4 pantallas y vive la experiencia multijugador en un mismo juego.

![Modos de juego](Imagenes/05-modos.svg)

---

## Especificaciones

| | |
|---|---|
| **Pantallas** | 4 pantallas a color, 64 × 64 px (una por cara lateral) |
| **Plataforma** | Placas FPGA |
| **Controles** | Mando NES, teclado y mouse |
| **Conectores por cara** | 2 × NES, 2 × PS/2 |
| **Audio** | Parlante integrado con rejilla en cada cara |
| **Encendido** | Botón general de la fuente (parte superior) y botón individual por pantalla |
| **Ventilación** | Rejilla en la parte superior |
| **Base** | Soportes de apoyo estables |
| **Chasis** | Impresión 3D |

---

# Desarrollo conceptual y técnico del producto

## Desarrollo de Consola de Videojuegos - Electrónica Digital I


[![UNal](https://img.shields.io/badge/Universidad-Nacional%20de%20Colombia-003366.svg)](https://unal.edu.co)
[![Curso](https://img.shields.io/badge/Curso-Electr%C3%B3nica%20Digital%20I-green.svg)](https://github.com/cicamargoba/digital_UN/tree/main/2026_1)
[![HDL](https://img.shields.io/badge/Language-Verilog%20%7C%20C-blue.svg)](#módulos-del-sistema-y-mapa-de-memoria)



Repositorio principal de la organización enfocado en el diseño, arquitectura RTL y desarrollo de periféricos para la consola de juegos retro sobre FPGA.



<details open>
<summary><b>Tabla de Contenidos</b></summary>

* [Modelo Físico](#modelo-físico)
* [Especificaciones del Proyecto](#especificaciones-del-proyecto)
* [Diagramas de Flujo](#diagramas-de-flujo)

</details>



## Modelo Físico


![Un primer vistazo](Render/ConsolaCopcepto-1.png)

La consola KUBIX estará compuesta por los elementos electrónicos y estructurales necesarios para su funcionamiento. En su interior contará con las entradas y conexiones previamente definidas, una fuente de alimentación encargada de suministrar energía al sistema y las pantallas que conformarán la interfaz visual de la consola. La estructura exterior estará fabricada mediante una combinación de piezas de acrílico y componentes elaborados mediante impresión 3D en filamento, buscando proporcionar resistencia, estabilidad y una apariencia adecuada al diseño. Finalmente, las diferentes partes de la estructura serán ensambladas y aseguradas mediante pines y tornillos, permitiendo mantener un montaje firme y, al mismo tiempo, facilitar el acceso a los componentes internos cuando sea necesario.



## Documentacion y bocetacion propuesta

-[Visual fisica por secciones de KUBIX](BocetoKUBIX/Armado%20de%20consola.pdf)
-[Tapa exterior](BocetoKUBIX/Tapa%20Exterior.pdf)
-[Tapa inferior](BocetoKUBIX/Tapa%20Inferior.pdf)
-[Soportes y contornos](BocetoKUBIX/Soportes%20y%20laina%20de%20pantalla.pdf)
-[Perspectiva 1](BocetoKUBIX/Completo1.idw) 
-[Perspectiva 2](BocetoKUBIX/Completo1.ipt) 


## Especificaciones del Proyecto

El proyecto consiste en el desarrollo de una consola de juegos retro construida de forma colaborativa sobre una arquitectura SoC en FPGA. El sistema utiliza un procesador RISC-V de 32 bits (RV32I / femtorv32) ejecutado como caja negra, el cual corre la lógica principal del juego programada en C y controla cada uno de los periféricos en hardware mediante un bus de direcciones y registros mapeados en memoria. Para la salida visual, la consola implementa una arquitectura distribuida de 4 pantallas independientes, donde cada una dispone de su propia FPGA dedicada para el procesamiento y renderizado gráfico.

La interacción con el usuario soporta múltiples controles de entrada, incluyendo mandos tradicionales de NES (`nes_controller.v`), así como teclado PS2 (`ps2_keyboard.v`) y ratón PS2 (`ps2_mouse`). La ejecución y almacenamiento de software se apoya en la memoria interna BRAM para el arranque y firma del sistema, junto con una memoria SPI Flash (`spi_flash_ctrl`) dedicada a guardar los juegos y otra memoria SPI RAM (`spiram_ctrl.v`) para la ejecución de procesos. Adicionalmente, el sistema incluye comunicación en red por puerto serial UART (`MultijugadorRed`) para conectar consolas y jugar en pareja, salida de audio digital I2S (`I2S_tx.v`), control de pantalla (`Display-Driver`) y una matriz LED (`MAX7219-`) para visualización de puntajes e indicadores.




## Diagramas de Flujo

### 1. Diagrama Central
Flujo de control general y secuencia de funcionamiento del sistema.



<img width="977" height="1540" alt="Diagrama_Flujo_General" src="https://github.com/user-attachments/assets/7e0558ab-2d74-4192-b621-2d45bf82a44a" />

### 2. Propuesta A: Lógica del Juego Integrada
---
Propuesta que incluye el procesamiento de la lógica del juego dentro del flujo principal de control.

![Diagrama Lógica de Juegos](https://raw.githubusercontent.com/noNintendo2026/nes_controller.v/main/img/diagrama_logica_juegos.drawio.png)


```
QGame- KUBIX/


```

<!-- Agregar: Diagrama de flujo general del proyecto, diagramas especificos de caseccion por asignacion de grupo, diagramas de bloques y de mas que consideremos   -->

---

## Equipo

Proyecto de **Electrónica Digital 1**, Ingeniería Eléctrica, Universidad Nacional de Colombia.

| Integrante | Rol |
|---|---|
| Daniel Eduardo Ballén Baena | SPI_RAM |
| _Nombre_ | _Rol_ |
| _Nombre_ | _Rol_ |
| _Nombre_ | _Rol_ |




