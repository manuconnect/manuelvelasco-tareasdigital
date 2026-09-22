```mermaid```

flowchart TD
    %% Estilos de bloques
    classDef estado fill:#e1d5e7,stroke:#9673a6,stroke-width:2px,color:#000;
    classDef accion fill:#dae8fc,stroke:#6c8ebf,stroke-width:2px,color:#000;
    classDef decision fill:#fff2cc,stroke:#d6b656,stroke-width:2px,color:#000;
    classDef externo fill:#d5e8d4,stroke:#82b366,stroke-width:2px,color:#000;

    %% Flujo
    S([Estado 0: IDLE / Espera]):::estado --> L[Estado 1: LATCH]:::estado
    
    L -->|LATCH = Alto| T1[Esperar 12 µs]:::accion
    T1 -->|LATCH = Bajo| C[Estado 2: LECTURA SERIAL]:::estado
    
    C --> Init[Bit a leer: n = 0]:::accion
    
    %% Bucle de lectura
    Init --> Read[/Leer pin DATA y guardar en Registro temporal bit 'n'/]:::externo
    Read --> CLK_H[CLOCK = Alto]:::accion
    CLK_H --> T2[Esperar 6 µs]:::accion
    T2 --> CLK_L[CLOCK = Bajo]:::accion
    CLK_L --> T3[Esperar 6 µs]:::accion
    T3 --> Inc[Siguiente bit: n = n + 1]:::accion
    
    Inc --> Cond{¿n == 8?}:::decision
    
    Cond -- NO (Faltan botones) --> Read
    
    %% Finalización
    Cond -- SÍ (Lectura completa) --> Done[Estado 3: ACTUALIZAR BUS]:::estado
    Done --> Update[Copiar Registro temporal al buzón 0x450000]:::externo
    Update --> Wait60Hz[Esperar ~16.6 ms para sincronizar a 60 FPS]:::accion
    Wait60Hz --> S
