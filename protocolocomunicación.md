```mermaid
flowchart TD
    %% Estilos
    classDef inicio fill:#e1d5e7,stroke:#9673a6,stroke-width:2px,color:#000;
    classDef accion fill:#dae8fc,stroke:#6c8ebf,stroke-width:2px,color:#000;
    classDef loop fill:#d5e8d4,stroke:#82b366,stroke-width:2px,color:#000;
    classDef decision fill:#fff2cc,stroke:#d6b656,stroke-width:2px,color:#000;

    Start([Estado de Reposo]):::inicio --> S0[LATCH = 0<br>CLOCK = 0]:::accion
    
    %% Fase 1: Tomar la Foto (Solo 1 vez)
    S0 -->|Iniciar lectura| S1[LATCH = 1]:::accion
    S1 --> S2[Esperar 12 µs]:::accion
    S2 --> S3[LATCH = 0]:::accion
    
    %% Preparar el bucle
    S3 --> Init[Iniciar contador:<br>n = 0]:::accion
    
    %% Fase 2: Ciclo de Lectura
    Init --> Read[Leer pin DATA y<br>guardar botón 'n']:::loop
    Read --> Inc[n = n + 1]:::loop
    
    Inc --> Cond{¿n == 8?}:::decision
    
    %% Repetición (Falta leer botones)
    Cond -- NO (Continúa) --> Clk1[CLOCK = 1]:::loop
    Clk1 --> W1[Esperar 6 µs]:::loop
    W1 --> Clk0[CLOCK = 0]:::loop
    Clk0 --> W2[Esperar 6 µs]:::loop
    W2 --> Read
    
    %% Fase 3: Terminar
    Cond -- SÍ (Terminó) --> Save[Guardar los 8 botones<br>en memoria]:::accion
    Save --> Wait[Esperar 16 ms<br>hasta el próximo frame]:::accion
    Wait --> Start
