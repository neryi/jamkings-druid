# Druiden Makros

Hier sind einige Makro Beispiele. Die Ränge und Namen nach Bedarf anpassen (besonders wenn der Englische Client verwendet wird).

## Shapeshifting / Powershift
- Ersetzen die normalen Zauber zum Formen wechseln.
- Erlauben direkt (separater global cooldown) von einer Form in die andere zu wechseln, oder beritten in Form.
- Funktionieren auch zum Powershift (Wolfskopfhelm oder Ingrimm rein/raus um Wut oder Energie zu generieren)

### Terrorbär 
Für den normalen Bär Name anpassen.
```lua
#showtooltip Terrorbärengestalt(Gestaltwandel)
/dismount [mounted]
/cancelform [noform:1]
/cast Terrorbärengestalt(Gestaltwandel)
```

### Katze
```lua
#showtooltip Katzengestalt(Gestaltwandel)
/dismount [mounted]
/cancelform [noform:3]
/cast Katzengestalt(Gestaltwandel)
```

### Wasser
```lua
#showtooltip Reisegestalt(Gestaltwandel)
/dismount [mounted]
/cancelform [noform:4]
/cast Reisegestalt(Gestaltwandel)
```

### Reise
```lua
#showtooltip Wassergestalt(Gestaltwandel)
/dismount [mounted]
/cancelform [noform:2]
/cast Wassergestalt(Gestaltwandel)
```

## Dust Makros
Dust Makros, im Anlehnung an die Staubwolke die beim wechseln von Formen angezeigt wird, kann man verwenden um Items in Gestalten benutzbar zu machen.
Da Gegestände auf separatem cooldown liegen, kann rausgewechselt, verwendet und wieder reingewechselt werden ohne warten zu müssen.

### Beispiel: Heiltrank in Bärform
```lua
/showtooltip
/cancelform
/use Heiltrank
/cast Terrorbärengestalt
```


## Downranking
Einige Beispiele wie man verschiedene Ränge eines Zaubers (downranking) mit modifier in ein einzelnes Makro packen kann.
Normales drücken verwendet den aktuell höchsten Rang. Hält man ctrl gedrückt ist es -1 Rang, alt (-2) oder shift (-3).
Denkt daran die jeweiligen Ränge je nach eurem Level oder Bedarf anzupassen.

Es empfiehlt sich beim ersten (nomod) keinen spezifischen Rang anzugeben. Dadurch wird automatisch der höchste verwendet. Dass hat den Vorteil das man auch niedrigstufige Spieler (bei denen der höchste nicht funktioniert) heilen kann, da WoW automatisch anpasst, sofern kein Rang angegeben wurde.

### Heilende Berührung
```lua
#showtooltip Heilende Berührung
/cast [nomod] Heilende Berührung
/cast [mod:ctrl] Heilende Berührung(Rang 7)
/cast [mod:alt] Heilende Berührung(Rang 6)
/cast [mod:shift] Heilende Berührung(Rang 5)
```
### Nachwachsen
```lua
#showtooltip Nachwachsen
/cast [nomod] Nachwachsen
/cast [mod:ctrl] Nachwachsen(Rang 5)
/cast [mod:alt] Nachwachsen(Rang 4)
/cast [mod:shift] Nachwachsen(Rang 3)
```
### Verjüngung
```lua
#showtooltip Verjüngung
/cast [nomod] Verjüngung
/cast [mod:ctrl] Verjüngung(Rang 7)
/cast [mod:alt] Verjüngung(Rang 6)
/cast [mod:shift] Verjüngung(Rang 5)
```


## Nützliches/Diverses

**Verheeren und Schreddern**  
Kombiniert Verheeren und Schreddern zu einer einzigen Funktion. 
Ist man beim Schleichen wird Verheeren verwendet, ansonsten Schreddern. 
```lua
#showtooltip Schreddern
/cast [stealth] Verheeren
/cast [nostealth] Schreddern 
```

**Feenfeuer in jeder Form**  
Verwendet je nach Form Feenfeuer oder Feenfeuer (Tiergestalt) (funktioniert natürlich nur wenn ihr dass Feenfeuer (Tiergestalt) Talent habt). 
```lua
#showtooltip Feenfeuer
/cast [nostance][stance:2][stance:4] Feenfeuer
/cast [stance:1][stance:3] Feenfeuer (Tiergestalt)
```

**Innervate Healer**  
Verlässt die Form und gibt Anregen auf Heiler, ohne z.B. als Tank, dass Ziel zu verlieren. Wechselt optional danach wieder zum Bär.  
*WICHTIG, Name des Heilers (HEALERNAME) vorher anpassen*

```lua
#showtooltip Anregen
/cancelform
/target HEALERNAME
/castsequence reset=combat/8  Anregen, Terrorbärengestalt(Gestaltwandel), null
/targetlasttarget
```

**Baumrinde + Heal**  
Aktuelle Form verlassen, Baumrinde + selbst heilen ohne Ziel zu verlieren.
```lua
#showtooltip Baumrinde
/cancelform
/castsequence [target=player] reset=combat/8  Baumrinde, Heilende Berührung
/targetlasttarget
```

## Rotations (sequence)
`castsequence` kann verwendet werden um Aktionen aneinander zu reihen. 

Hier ein simples Beispiel wie eine Sequenz erstellt werden kann.

Dabei wird in Katzenform erst Feenfeuer und Krallenhieb gesetzt, danach mit Klaue 5 Combo Punkte aufgebaut um Zerfetzen zu verwenden. 

Durch `reset=combat/20/target` wird das Macro bei jedem neuen Kampf, Zielwechsel oder nach 20 Sekunden ohne Verwendung wieder zurückgesetzt.
```lua
#showtooltip Krallenhieb
/castsequence reset=combat/20/target Feenfeuer (Tiergestalt), Krallenhieb, Klaue, Klaue, Klaue, Krallenhieb, Zerfetzen, Klaue, Klaue, Klaue, Klaue, Krallenhieb, Zerfetzen, Klaue, Klaue, Klaue
```

