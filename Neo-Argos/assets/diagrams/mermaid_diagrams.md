
# Diagrama de Arquitectura de Hardware y Comunicación

``` mermaid
graph TB
    subgraph Estacion_Remota [Estación de Control]
        Laptop(Laptop / Workstation)
    end

    subgraph Neo_Argos_Robot [Neo-Argos AMR - TRL 4]
        subgraph Computo_Alto_Nivel [Capa de Procesamiento]
            Jetson[NVIDIA Jetson Orin Nano 8GB]
            Lidar[RPLidar A1M8]
            Camera[Intel RealSense D435i]
        end

        subgraph Capa_Control [Neo-Control Shield v1.0]
            ESP32[ESP32 MCU]
            CAN_Mod[MCP2515 CAN Controller]
        end

        subgraph Actuacion [Capa de Actuación]
            M1[Motor AK10-9 L]
            M2[Motor AK10-9 R]
        end
    end

    %% Conexiones
    Laptop -- "WiFi (SSH / ROS 2 DDS)" --> Jetson
    Jetson -- "USB" --> Lidar
    Jetson -- "USB" --> Camera
    Jetson -- "UART (micro-ROS Agent)" --> ESP32
    ESP32 -- "SPI" --> CAN_Mod
    CAN_Mod -- "CAN Bus (AK_Motors_Lib)" --> M1
    CAN_Mod -- "CAN Bus (AK_Motors_Lib)" --> M2

    style Neo_Argos_Robot fill:#f9f9f9,stroke:#333,stroke-width:2px
    style Jetson fill:#76b900,color:#fff
    style ESP32 fill:#e67e22,color:#fff
```

# Diagrama de Software (Grafo Computacional ROS 2)

``` mermaid
graph LR
    subgraph Sensores
        S1[RPLidar Node]
        S2[RealSense Node]
    end

    subgraph Localizacion [Fusión y Estimación]
        SLAM[SLAM Toolbox]
        EKF[robot_localization EKF]
    end

    subgraph Navegacion [Nav2 Stack]
        Plan[Planner / Controller]
        BT[Behavior Trees]
    end

    subgraph Low_Level [Capa de Hardware]
        Agent[micro-ROS Agent]
        Firmware[ESP32 Firmware]
    end

    %% Flujo de Datos
    S1 -- "/scan" --> SLAM
    S1 -- "/scan" --> Plan
    S2 -- "/imu" --> EKF
    SLAM -- "map -> odom (tf)" --> EKF
    EKF -- "odom -> base_link (tf)" --> Plan
    
    Plan -- "/cmd_vel" --> Agent
    Agent -- "Serial /transports" --> Firmware
    Firmware -- "CAN commands" --> Actuadores((Motores))

    style Navegacion fill:#d1eaf0
    style Localizacion fill:#d1f0d1
```

# Diagrama de Topología de Potencia

``` mermaid
graph TD
    subgraph Sistema_Baterias [Alimentación On-board]
        Bat1[LiPo 6S 22.2V 6000mAh]
        Bat2[LiPo 6S 22.2V]
        Bat3[LiPo 6S 22.2V]
        Series[Baterías en Serie 48V]
        Bat2 --- Series
        Bat3 --- Series
    end

    subgraph Distribucion [Neo-Power Board v1.0]
        Reg19[Regulador DC-DC 19V]
        EStop1[Interruptor Mecánico 1]
        EStop2[Interruptor Mecánico 2]
    end

    subgraph Cargas [Consumo]
        Jetson[Jetson Orin Nano]
        Perif[Lidar / Cámara / ESP32]
        Motors[Motores AK10 High-Torque]
    end

    %% Conexiones Eléctricas
    Bat1 --> EStop1
    EStop1 --> Reg19
    Reg19 --> Jetson
    Jetson -- "USB Power" --> Perif

    Series --> EStop2
    EStop2 --> Motors

    style Series fill:#f66,color:#fff
    style Reg19 fill:#3498db,color:#fff
```

# Diagrama Integrado: Arquitectura de Potencia e Interfazado

``` mermaid

graph TD
    subgraph Suministro_Energia [Sistema de Baterías]
        B1[Batería Logic: LiPo 6S 22.2V]
        subgraph Serie_Motores [Banco de Potencia 44.4V - 48V]
            B2[Batería Motor A: 6S]
            B3[Batería Motor B: 6S]
            B2 --- B3
        end
        GND_Ref((Punto de Tierra Común))
        B1 -.-> GND_Ref
        B2 -.-> GND_Ref
    end

    subgraph Power_Distribution [Neo-Power Board v1.0]
        Reg19[Regulador Buck-Boost 19V]
        SW_Logic[Interruptor Lógica]
        SW_Power[Interruptor Potencia]
    end

    subgraph Control_Core [Neo-Control Shield v1.0]
        ESP32[ESP32 Microcontroller]
        MCP[MCP2515 CAN Controller]
    end

    subgraph Computing [Capa de Procesamiento]
        Jetson[NVIDIA Jetson Orin Nano]
        Lidar[RPLidar A1M8]
        Cam[Intel RealSense D435i]
    end

    subgraph Actuadores [Tren Motriz]
        M1[Motor AK10-9 L]
        M2[Motor AK10-9 R]
    end

    %% Conexiones Eléctricas
    B1 --> SW_Logic --> Reg19 --> Jetson
    Serie_Motores --> SW_Power --> M1 & M2

    %% Conexiones de Datos e Interfazado
    Jetson -- "USB (Power + Data)" --> Lidar & Cam
    Jetson -- "UART / Serial (micro-ROS)" --> ESP32
    ESP32 -- "SPI Protocol" --> MCP
    MCP -- "CAN Bus (Shared GND)" --> M1 & M2

    %% Estilos
    style GND_Ref fill:#333,stroke:#fff,color:#fff
    style B1 fill:#f9f,stroke:#333
    style Serie_Motores fill:#f96,stroke:#333
    style Jetson fill:#76b900,color:#fff
    style ESP32 fill:#e67e22,color:#fff

```

# Diagrama de Bloques Funcionales (Fisico-Lógico)

``` mermaid

graph LR
    subgraph "Nivel 3: Percepción y Cognición (Jetson)"
        A1[SLAM Toolbox] --- A2[Nav2 Stack]
        A2 --- A3[Robot Localization]
    end

    subgraph "Nivel 2: Abstracción de Hardware (ESP32 / micro-ROS)"
        B1[micro-ROS Agent] <--> B2[CAN_Motors_Library]
        B2 <--> B3[Gestión de Odometría]
    end

    subgraph "Nivel 1: Capa Física (Chasis Neo-Argos)"
        C1[Estructura Aluminio CNC]
        C2[Ruedas / Tracción Diferencial]
        C3[Sensores LiDAR / IMU]
    end

    %% Relaciones de Dependencia
    A1 -.-> C3
    A2 -.-> B1
    B2 -.-> C2
    C3 -.-> A3

    style C1 fill:#3498db
    style C2 fill:#3498db

```