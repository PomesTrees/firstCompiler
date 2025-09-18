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
