# PracticaGIT


flowchart LR
  %% Sender
  subgraph Message_Sender["Message Sender"]
    style Message_Sender fill:#EEEEEE,stroke:#AAA,stroke-width:1px
    MSO["Microservicio Pedidos<br/>(Event Bus API)"]
  end

  %% RabbitMQ Container
  subgraph RabbitMQ["RabbitMQ<br/>(Server/Container)"]
    style RabbitMQ fill:#A4D65E,stroke:#333,stroke-width:2px
    direction TB
    Q1["Queue A<br/>pedido.creado"]
    Q2["Queue B<br/>despacho.listo_para_envio"]
  end

  %% Receivers
  subgraph Message_Receivers["Message Receivers"]
    style Message_Receivers fill:#EEEEEE,stroke:#AAA,stroke-width:1px
    MSA["Inventario Service<br/>(Event Bus API)"]
    MSB["Despachos Service<br/>(Event Bus API)"]
  end

  %% Flujos
  MSO -- publica pedido.creado --> Q1
  Q1 -- subscribe & consume --> MSA

  MSO -- publica despacho.listo_para_envio --> Q2
  Q2 -- subscribe & consume --> MSB
