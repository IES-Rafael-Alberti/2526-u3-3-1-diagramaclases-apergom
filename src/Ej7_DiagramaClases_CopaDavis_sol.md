# Solución: Ejercicio 7 - Diagrama de Clases - Copa Davis (Eliminatorias)

## Clases principales

- Equipo
  - -idEquipo: String
  - -nombre: String
  - -pais: String
  - +getJugadores(): List<Jugador>

- Jugador
  - -idJugador: String
  - -nombre: String
  - -ranking: int

- Eliminatoria
  - -id: String
  - -sede: String
  - -superficie: Superficie (enum: CESPED, TIERRA_BATIDA, PISTA_DURA)
  - -fecha: Date
  - +resultadoGlobal(): String

- Partido (abstracto)
  - -idPartido: String
  - -resultado: ResultadoPartido (enum: LOCAL, VISITANTE, INDEFINIDO)

- PartidoIndividual extends Partido
  - -jugadorLocal: Jugador
  - -jugadorVisitante: Jugador

- PartidoDobles extends Partido
  - -parejaLocal: List<Jugador> (2)
  - -parejaVisitante: List<Jugador> (2)

## Reglas y restricciones

- Eliminatoria contiene exactamente 5 Partidos (4 individuales + 1 dobles).
- Equipo tiene entre 1 y 5 jugadores inscritos para una eliminatoria.
- Gana la eliminatoria el equipo con >= 3 victorias.
- En individuales, jugadores deben pertenecer a equipos distintos.

## PlantUML

```plantuml
@startuml
enum Superficie { CESPED
TIERRA_BATIDA
PISTA_DURA }
enum Resultado { LOCAL
VISITANTE
INDEFINIDO }
class Equipo {
  -idEquipo: String
  -nombre: String
  -pais: String
  +getJugadores(): List<Jugador>
}
class Jugador {
  -idJugador: String
  -nombre: String
  -ranking: int
}
class Eliminatoria {
  -id: String
  -sede: String
  -superficie: Superficie
  -fecha: Date
  +resultadoGlobal(): String
}
abstract class Partido {
  -idPartido: String
  -resultado: Resultado
}
class PartidoIndividual
class PartidoDobles
Eliminatoria "1" *-- "5" Partido
Equipo "1" -- "1..5" Jugador : inscriben
PartidoIndividual -- Jugador : jugadorLocal
PartidoIndividual -- Jugador : jugadorVisitante
PartidoDobles "1" -- "2" Jugador : parejaLocal
PartidoDobles "1" -- "2" Jugador : parejaVisitante
@enduml
```