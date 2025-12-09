# Solución: Ejercicio 4 - Diagrama de Clases - Gestión Empresarial

## Clases principales

- Persona (abstracta)
  - -nombre: String
  - -fechaNacimiento: Date
  - +calcularEdad(): int

- Empleado extends Persona
  - -idEmpleado: String
  - -categoria: Categoria (enum: JUNIOR, SENIOR, MANAGER)
  - -sueldoBruto: double
  - +calcularSueldoNeto(): double
  - -responsable: Empleado (relación reflexiva)

- Cliente extends Persona
  - -idCliente: String
  - -email: String
  - +listarEmpresas(): List<Empresa>

- Empresa
  - -nombre: String
  - -cif: String
  - -direccionFiscal: String
  - +getContactos(): List<Cliente>

## Relaciones

- Empleado puede ser responsable de 0..* Empleado (relación reflexiva responsable_de).
- Empresa "1" -- "1..*" Cliente : tiene (cada cliente pertenece al menos a una empresa).
- Si un cliente representa a varias empresas, se puede modelar una asociación N:M Empresa<->Cliente con una clase intermedia si se necesitan datos extra.

## PlantUML

```plantuml
@startuml
enum Categoria { JUNIOR
SENIOR
MANAGER }
abstract class Persona {
  -nombre: String
  -fechaNacimiento: Date
  +calcularEdad(): int
}
class Empleado {
  -idEmpleado: String
  -categoria: Categoria
  -sueldoBruto: double
  +calcularSueldoNeto(): double
}
class Cliente {
  -idCliente: String
  -email: String
  +listarEmpresas(): List<Empresa>
}
class Empresa {
  -nombre: String
  -cif: String
  -direccionFiscal: String
  +getContactos(): List<Cliente>
}
Persona <|-- Empleado
Persona <|-- Cliente
Empleado "0..1" -- "0..*" Empleado : responsable_de
Empresa "1" -- "1..*" Cliente : tiene
@enduml
```