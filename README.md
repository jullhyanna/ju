# ju
```mermaid stateDiagram-v2
    direction TB
    
    [*] --> E_STOP
    
    E_STOP --> E_STOP : START = 0
    E_STOP --> E_COUNT_1 : START = 1
    
    state "Fase 1: Preparação (L1=1, L2=0, Motor=0)" as Fase1 {
        direction TB
        E_COUNT_1 --> E_COUNT_2 : 1s [Disp=2]
        E_COUNT_2 --> E_COUNT_3 : 1s [Disp=3]
    }
    
    E_COUNT_3 --> E_MOTOR_5 : 1s [Disp=5]
    
    state "Fase 2: Motor Ligado (L1=0, L2=1, Motor=1)" as Fase2 {
        direction TB
        E_MOTOR_5 --> E_MOTOR_4 : 1s [Disp=4]
        E_MOTOR_4 --> E_MOTOR_3 : 1s [Disp=3]
        E_MOTOR_3 --> E_MOTOR_2 : 1s [Disp=2]
        E_MOTOR_2 --> E_MOTOR_1 : 1s [Disp=1]
    }
    
    E_MOTOR_1 --> E_OFF_0 : 1s [Disp=0]
    
    state "Fase 3: Desligamento (L1=1, L2=0, Motor=0)" as Fase3 {
        direction TB
        E_OFF_0 --> E_OFF_1 : 1s [Disp=1]
        E_OFF_1 --> E_OFF_2 : 1s [Disp=2]
        E_OFF_2 --> E_OFF_3 : 1s [Disp=3]
    }
    
    E_OFF_3 --> E_STOP : 1s [Regresso ao repouso]
