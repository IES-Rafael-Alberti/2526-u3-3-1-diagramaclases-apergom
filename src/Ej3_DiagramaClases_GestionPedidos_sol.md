# Solución: Ejercicio 3 - Diagrama de Clases - Gestión de Pedidos

## Clases principales

- Pedido (abstracto)
  - -idPedido: String
  - -fecha: Date
  - -estado: EstadoPedido (enum: NUEVO, PROCESANDO, ENVIADO, ENTREGADO, CANCELADO)
  - +calcularTotal(): double

- PedidoSimple extends Pedido
  - -lineas: List<LineaPedido>

- PedidoCompuesto extends Pedido
  - -subPedidos: List<Pedido>

- LineaPedido (clase de asociación)
  - -cantidad: int
  - -precioUnitario: double
  - +getSubtotal(): double
  - Asociaciones a Producto y Pedido

- Producto
  - -codigo: String
  - -nombre: String
  - -descripcion: String
  - -precio: double

- ProcesadorCobros (Singleton)
  - <<singleton>>
  - +getInstance(): ProcesadorCobros
  - +procesarPago(pedido: Pedido): boolean

- Cliente
  - -idCliente: String
  - -nombre: String
  - -direccion: String

## Relaciones y patrones

- Pedido compuesto contiene sub-pedidos (composición).
- PedidoSimple contiene LineaPedido (composición).
- LineaPedido asocia Pedido <-> Producto (clase de asociación con atributos cantidad y precioUnitario).
- ProcesadorCobros marcado como <<singleton>>.

## PlantUML

```plantuml
@startuml
interface IProcesadorCobros {
  +procesarPago(pedido: Pedido): boolean
}
class ProcesadorCobros <<singleton>> {
  +getInstance(): ProcesadorCobros
  +procesarPago(pedido: Pedido): boolean
}
enum EstadoPedido { NUEVO
PROCESANDO
ENVIADO
ENTREGADO
CANCELADO }
abstract class Pedido {
  -idPedido: String
  -fecha: Date
  -estado: EstadoPedido
  +calcularTotal(): double
}
class PedidoSimple
class PedidoCompuesto
class LineaPedido {
  -cantidad: int
  -precioUnitario: double
  +getSubtotal(): double
}
class Producto {
  -codigo: String
  -nombre: String
  -descripcion: String
  -precio: double
}
class Cliente {
  -idCliente: String
  -nombre: String
  -direccion: String
}
Pedido <|-- PedidoSimple
Pedido <|-- PedidoCompuesto
PedidoCompuesto "1" *-- "0..*" Pedido : subPedidos
PedidoSimple "1" *-- "1..*" LineaPedido
LineaPedido "*" -- "1" Producto
Cliente "1" -- "0..*" Pedido
ProcesadorCobros ..|> IProcesadorCobros
@enduml
```