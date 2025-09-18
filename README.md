# ATM Example

```mermaid
flowchart TD
  A[Insert Card] --> B[Enter PIN]
  B --> C{PIN Valid?}
  C -->|Yes| D[Show Menu]
  C -->|No| E[Reject Card]

classDiagram
class Tarjeta {
  +pan: String
  +fechaExp: Date
  +estado: EstadoTarjeta
}

class Cuenta {
  +numero: String
  +saldoDisponible: Money
  +saldoContable: Money
  +debitar(monto): boolean
  +acreditar(monto): void
}

class Cliente {
  +id: String
  +nombre: String
}

class Transaccion {
  <<abstract>>
  +id: UUID
  +fechaHora: DateTime
  +monto: Money
  +ejecutar(): ResultadoTx
}

class Retiro extends Transaccion
class Deposito extends Transaccion
class ConsultaSaldo extends Transaccion
class PagoServicio extends Transaccion {
  +servicio: String
  +referencia: String
}

class ATM {
  +id: String
  +ubicacion: String
}

class Sesion {
  +inicio: DateTime
  +estado: EstadoSesion
  +finalizar(): void
}

class HostBancario {
  +autenticar(pan,pin): bool
  +autorizar(tx): Autorizacion
  +registrar(tx): void
}

Cliente "1" -- "0..*" Tarjeta
Tarjeta "1" --> "1" Cuenta : asociada a
Cuenta "1" <-- "0..*" Transaccion
ATM "1" o-- "1" Sesion
ATM "1" --> "1" HostBancario : ISO8583/API

Retiro --> Cuenta : debitar()
Deposito --> Cuenta : acreditar()
ConsultaSaldo --> Cuenta
PagoServicio --> Cuenta
