# Solución: Ejercicio 2 - Diagrama de Clases - Cursos Universitarios

## Clases principales

1. Curso
   - Atributos (privados):
     - -codigo: String
     - -nombre: String
     - -descripcion: String
     - -creditos: int
     - -nivel: Nivel (enum: GRADO, MASTER, DOCTORADO)
   - Métodos:
     - +getNumMatriculados(): int

2. Profesor
   - Atributos:
     - -idEmpleado: String
     - -nombreCompleto: String
     - -email: String
     - -departamento: String
   - Métodos:
     - +impartirClase()
     - +prepararExamen()
     - +evaluarEstudiante()

3. Estudiante
   - Atributos:
     - -numExpediente: String
     - -nombreCompleto: String
     - -email: String
     - -fechaMatriculaUniversidad: Date
   - Métodos:
     - +asistir()
     - +estudiar()
     - +presentarseExamen()

4. Matricula (clase de asociación)
   - Atributos:
     - -fechaMatricula: Date
     - -nota: Double (nullable)
   - Métodos:
     - +actualizarNota(n: Double)

## Relaciones y cardinalidades

- Profesor "1" --- "0..*" Curso : responsable_de
  - Un curso tiene un único profesor responsable; un profesor puede impartir varios cursos.
- Curso "1" --- "0..*" Matricula --- "0..*" Estudiante
  - Matricula liga Curso y Estudiante y almacena fecha y nota.
- Estudiante y Curso se relacionan N:M a través de Matricula.

## PlantUML

```plantuml
@startuml
enum Nivel { GRADO
MASTER
DOCTORADO }
class Curso {
  -codigo: String
  -nombre: String
  -descripcion: String
  -creditos: int
  -nivel: Nivel
  +getNumMatriculados(): int
}
class Profesor {
  -idEmpleado: String
  -nombreCompleto: String
  -email: String
  -departamento: String
  +impartirClase()
  +prepararExamen()
  +evaluarEstudiante()
}
class Estudiante {
  -numExpediente: String
  -nombreCompleto: String
  -email: String
  -fechaMatriculaUniversidad: Date
  +asistir()
  +estudiar()
  +presentarseExamen()
}
class Matricula {
  -fechaMatricula: Date
  -nota: Double
  +actualizarNota(n: Double)
}
Profesor "1" -- "0..*" Curso : responsable_de
Curso "1" -- "0..*" Matricula
Estudiante "0..*" -- "0..*" Matricula
Matricula --> Curso
Matricula --> Estudiante
@enduml
```