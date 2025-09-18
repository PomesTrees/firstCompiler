# UML del Cajero Automático (ATM)

Este documento muestra los diagramas UML del sistema de cajero automático siguiendo el modelo **4+1 vistas** de Kruchten.

---

## 1. Vista de Escenarios (Casos de Uso)

```mermaid
%% Diagrama de casos de uso
flowchart TB
  actor1([Cliente])
  actor2([Banco/Host])
  
  subgraph ATM
    CU1([Consultar saldo])
    CU2([Retirar efectivo])
    CU3([Depositar dinero])
    CU4([Pagar servicio])
  end

  actor1 --> CU1
  actor1 --> CU2
  actor1 --> CU3
  actor1 --> CU4
  
  CU1 --> actor2
  CU2 --> actor2
  CU3 --> actor2
  CU4 --> actor2

%% Diagrama de clases simplificado
classDiagram
  class Cliente {
    +id: String
    +nombre: String
  }
  class Cuenta {
    +numero: String
    +saldo: float
    +debitar(monto)
    +acreditar(monto)
  }
  class Tarjeta {
    +pan: String
    +expira: Date
  }
  class Transaccion {
    <<abstract>>
    +id: int
    +fecha: Date
    +monto: float
    +ejecutar()
  }
  class Retiro
  class Deposito
  class ConsultaSaldo
  class PagoServicio

  Cliente "1" -- "0..*" Tarjeta
  Tarjeta "1" --> "1" Cuenta
  Cuenta "1" <-- "0..*" Transaccion
  Retiro --|> Transaccion
  Deposito --|> Transaccion
  ConsultaSaldo --|> Transaccion
  PagoServicio --|> Transaccion
