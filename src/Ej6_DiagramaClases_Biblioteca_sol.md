# Solución: Ejercicio 6 - Diagrama de Clases - Biblioteca

## Clases principales

- Libro
  - -id: String
  - -titulo: String
  - -autor: String
  - -tipo: TipoLibro (enum: NOVELA, POESIA, CUENTOS)
  - -estado: EstadoLibro (enum: DISPONIBLE, PRESTADO, RETRASADO)
  - +cambiarEstado(nuevo: EstadoLibro): void

- Socio
  - -idSocio: String
  - -nombre: String
  - -fechaNacimiento: Date
  - +tieneMultaActiva(): boolean
  - +numPrestamosActivos(): int

- Prestamo (clase de asociación entre Socio y Libro)
  - -fechaPrestamo: Date
  - -fechaLimite: Date {derived = fechaPrestamo + 30d}
  - -fechaDevolucion: Date (nullable)
  - +calcularDiasRetraso(): int

- Multa
  - -fechaInicio: Date
  - -diasMulta: int

## Reglas y validaciones (resumidas)

- Al prestar: comprobar !socio.tieneMultaActiva() && socio.numPrestamosActivos() < 3 && libro.estado == DISPONIBLE.
- Al devolver: buscar Prestamo activo; si fechaDevolucion > fechaLimite, generar Multa con dias = 3 * diasRetraso; además cambiar estado del libro a DISPONIBLE o RETRASADO según corresponda.

## PlantUML

```plantuml
@startuml
enum TipoLibro { NOVELA
POESIA
CUENTOS }
enum EstadoLibro { DISPONIBLE
PRESTADO
RETRASADO }
class Libro {
  -id: String
  -titulo: String
  -autor: String
  -tipo: TipoLibro
  -estado: EstadoLibro
  +cambiarEstado(nuevo: EstadoLibro): void
}
class Socio {
  -idSocio: String
  -nombre: String
  -fechaNacimiento: Date
  +tieneMultaActiva(): boolean
  +numPrestamosActivos(): int
}
class Prestamo {
  -fechaPrestamo: Date
  -fechaLimite: Date
  -fechaDevolucion: Date
  +calcularDiasRetraso(): int
}
class Multa {
  -fechaInicio: Date
  -diasMulta: int
}
Socio "1" -- "0..*" Prestamo
Libro "1" -- "0..*" Prestamo
Prestamo "0..1" -- "0..*" Multa
@enduml
```