# Konzepte der IT

**Prüfung:** 28.10.2022

**Telefon:** (01) 58801 38434

**Notenzusammensetzung**: Module + Übungen + Labor => Test


# Digitaltechnik
* Zahlensystem zur Basis 2
* Größte relative Differenz
* m = 2^n
* Bit 1 || 0
* Byte = Bit[8]
* Relativ Störungsunanfällig

## AND
| A | B | R |
| - | - | - |
| 0 | 0 | 0 |
| 0 | 1 | 0 |
| 1 | 0 | 0 |
| 1 | 1 | 1 |

## OR
| A | B | R |
| - | - | - |
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 1 |

## XOR
| A | B | R |
| - | - | - |
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 0 |


## NOT
| A | R |
| - | - |
| 0 | 1 |
| 1 | 0 |

## Schaltnetzanalyse
* Wahrheitstabelle (WT)
* Stellen = 2^Eingabewerte
* Schaltnetze haben immer eine Verzögerung (annahme Trotzdem ~= 0)
  
## Morgan'sche Gesetze
  A && B = !(!A || !B)

  A || B = !(!A && !B)


## Schaltungssynthese
Generieren eines Schaltnetzes aus einer gewünschten Wahrheitstabelle
### Disjunktive Normalform
1. Mittels Vollkonjunktion und negationen die Gewünschten positiven Einzelergebnisse erzeugen
2. Mittels Or-Gatter Teilergebnisse aggregieren
3. Minimierung durch verknüpfung "logischer Nachbarn" (Kombinationen, die unabhängig von den anderen Eingängen die gleichen Ergebnisse produzieren) - Karnaugh-Veitch-Diagramm

