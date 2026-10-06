# Desarrollo de Consola de Videojuegos - Electrónica Digital I


[![UNal](https://img.shields.io/badge/Universidad-Nacional%20de%20Colombia-003366.svg)](https://unal.edu.co)
[![Curso](https://img.shields.io/badge/Curso-Electr%C3%B3nica%20Digital%20I-green.svg)](https://github.com/cicamargoba/digital_UN/tree/main/2026_1)
[![HDL](https://img.shields.io/badge/Language-Verilog%20%7C%20C-blue.svg)](#módulos-del-sistema-y-mapa-de-memoria)



Repositorio principal de la organización enfocado en el diseño, arquitectura RTL y desarrollo de periféricos para la consola de juegos retro sobre FPGA.



<details open>
<summary><b>Tabla de Contenidos</b></summary>

* [Modelo Físico](#modelo-físico)
* [Especificaciones del Proyecto](#especificaciones-del-proyecto)
* [Módulos del Sistema y Mapa de Memoria](#módulos-del-sistema-y-mapa-de-memoria)
* [Diagramas de Flujo](#diagramas-de-flujo)

</details>



## Modelo Físico
---

Espacio reservado para la descripción, especificaciones de la carcasa/chasis y vistas del modelo físico de la consola.


## Especificaciones del Proyecto

El proyecto consiste en el desarrollo de una consola de juegos retro construida de forma colaborativa sobre una arquitectura SoC en FPGA. El sistema utiliza un procesador RISC-V de 32 bits (RV32I / femtorv32) ejecutado como caja negra, el cual corre la lógica principal del juego programada en C y controla cada uno de los periféricos en hardware mediante un bus de direcciones y registros mapeados en memoria. Para la salida visual, la consola implementa una arquitectura distribuida de 4 pantallas independientes, donde cada una dispone de su propia FPGA dedicada para el procesamiento y renderizado gráfico.

La interacción con el usuario soporta múltiples controles de entrada, incluyendo mandos tradicionales de NES (`nes_controller.v`), así como teclado PS2 (`ps2_keyboard.v`) y ratón PS2 (`ps2_mouse`). La ejecución y almacenamiento de software se apoya en la memoria interna BRAM para el arranque y firma del sistema, junto con una memoria SPI Flash (`spi_flash_ctrl`) dedicada a guardar los juegos y otra memoria SPI RAM (`spiram_ctrl.v`) para la ejecución de procesos. Adicionalmente, el sistema incluye comunicación en red por puerto serial UART (`MultijugadorRed`) para conectar consolas y jugar en pareja, salida de audio digital I2S (`I2S_tx.v`), control de pantalla (`Display-Driver`) y una matriz LED (`MAX7219-`) para visualización de puntajes e indicadores.



## Módulos del Sistema y Mapa de Memoria
---

A continuación se presentan los submódulos de la organización junto con su dirección correspondiente dentro del mapa de memoria del SoC:

| Repositorio / Módulo | Rango de Memoria | Descripción |
| :--- | :--- | :--- |
| `software_juegos` | `0x000000 - 0x3FFFFF` | BRAM para arranque, firmware y código fuente de los juegos. |
| `UART` | `0x400000 - 0x40FFFF` | Protocolo de comunicación UART base para depuración. |
| `spi_flash_ctrl` | `0x420000 - 0x42FFFF` | Controlador para la memoria SPI Flash de almacenamiento. |
| `ps2_keyboard.v` | `0x430000 - 0x43FFFF` | Driver y control para teclado PS2. |
| `ps2_mouse` | `0x440000 - 0x44FFFF` | Driver para [Raton PS2](https://github.com/noNintendo2026/ps2_mouse) |
| `nes_controller.v` | `0x450000 - 0x45FFFF` | Driver para controles de NES. |
| `I2C_Master` | `0x460000 - 0x46FFFF` | Módulo I2C Master para almacenamiento de puntajes y periféricos. |
| `I2S_tx.v` | `0x470000 - 0x47FFFF` | Transmisor de audio digital I2S. |
| `Display-Driver` | `0x480000 - 0x4FFFFF` | Driver para la gestión de pantalla, framebuffer y gráficos. |
| `spiram_ctrl.v` | Por determinar | Controlador para la gestión de memoria RAM necesaria para la ejecución de procesos |
| `MAX7219-` | Auxiliar | Controlador para la matriz de LEDs. |
| `MultijugadorRed` | Auxiliar | Módulo de comunicación por Serial I/O para partidas multijugador. |
| `.github` | N/A | Proyecto general del cubo de juegos con soporte de mandos. |
| `defaultTemplate` | N/A | Plantilla base para desarrollar módulos individuales. |



## Diagramas de Flujo

### 1. Diagrama Central
Flujo de control general y secuencia de funcionamiento del sistema.

![Diagrama General](https://raw.githubusercontent.com/noNintendo2026/nes_controller.v/main/img/diagrama_general.drawio.png)


### 2. Propuesta A: Lógica del Juego Integrada
---
Propuesta que incluye el procesamiento de la lógica del juego dentro del flujo principal de control.

![Diagrama Lógica de Juegos](https://raw.githubusercontent.com/noNintendo2026/nes_controller.v/main/img/diagrama_logica_juegos.drawio.png)



