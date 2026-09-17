# manuelvelasco-tareasdigital
Repositorio creado con la finalidad de subir las tareas realizadas por el estudiante Manuel Alejandro Velasco Marinez, para el curso de Electrónica Digital I

```mermaid
flowchart TD
    %% Definición de colores
    classDef verde fill:#d5e8d4,stroke:#82b366,color:#000000;
    classDef azul fill:#dae8fc,stroke:#6c8ebf,color:#000000;
    classDef amarillo fill:#fff2cc,stroke:#d6b656,color:#000000;
    classDef rojo fill:#f8cecc,stroke:#b85450,color:#000000;
    classDef morado fill:#e1d5e7,stroke:#9673a6,color:#000000;

    A([Inicio: Encendido y Reset de FPGA]):::verde
    B[Carga de Firmware e Inicialización RV32I]:::azul
    C[Diagnóstico del Bus de Memoria y Periféricos]:::azul
    D{¿Periféricos listos?}:::amarillo
    E[Estado de Error: LED Rojo]:::rojo
    F[Desplegar Menú Principal - Pantalla LED]:::azul
    G[Leer Registros de Entrada - Bus de Datos]:::morado
    H{¿Acción del Jugador?}:::amarillo
    I[Game Loop: Lógica en C y Actualización de Pantalla/Audio]:::azul
    J{¿Juego Terminado / Pausa?}:::amarillo

    A --> B
    B --> C
    C --> D
    D -- No --> E
    D -- Sí --> F
    F --> G
    G --> H
    H -- No --> G
    H -- Sí --> I
    I --> J
    J -- No --> G
    J -- Sí --> F
