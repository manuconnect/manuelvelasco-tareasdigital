# manuelvelasco-tareasdigital
Repositorio creado con la finalidad de subir las tareas realizadas por el estudiante Manuel Alejandro Velasco Marinez, para el curso de Electrónica Digital I

```mermaid
flowchart TD
    %% Estilos y paleta de colores
    classDef init fill:#e1f5fe,stroke:#0288d1,stroke-width:2px,color:#000;
    classDef menu fill:#fff3e0,stroke:#f57c00,stroke-width:2px,color:#000;
    classDef game fill:#e8f5e9,stroke:#388e3c,stroke-width:2px,color:#000;
    classDef err fill:#ffebee,stroke:#d32f2f,stroke-width:2px,color:#000;

    subgraph Etapa1 [1. Arranque y Diagnóstico]
        A([Encendido y Reset de FPGA]):::init --> B[Cargar Firmware desde BRAM]:::init
        B --> C{¿Hardware y Periféricos ok?}:::init
        C -- No --> D[Bloquear Sistema ]:::err
        C -- Sí --> E[Inicializar Display LED y Módulo de Audio]:::init
    end

    subgraph Etapa2 [2. Navegación del Menú]
        E --> F[Renderizar Menú Principal]:::menu
        F --> G[/Leer Bus: Registro CSR del Control/]:::menu
        G --> H{¿Acción del Jugador?}:::menu
        H -- Mover Cursor --> I[Actualizar Selección en Pantalla]:::menu
        I --> G
    end

    subgraph Etapa3 [3. Bucle Principal del Juego]
        H -- Iniciar Juego --> J[Cargar Lógica y Gráficos del Juego Seleccionado]:::game
        J --> K[/Capturar Entradas en Tiempo Real/]:::game
        L --> M{¿Ocurre un Evento?}:::game
        K --> L[Calcular Posiciones]:::game
        M -- Sí --> N[Actualizar Puntaje/Vidas y Emitir Sonido]:::game
        M -- No --> O[Actualizar Framebuffer de Pantalla]:::game
        N --> O
        O --> P{¿Partida Terminada o Salida?}:::game
        P -- Continúa --> K
        P -- Fin de Juego --> F
    end
