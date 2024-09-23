## Conceptes bàsics de XML

XML (Extensible Markup Language) és un llenguatge de marques dissenyat per emmagatzemar i transportar dades de manera estructurada. A continuació es detallen alguns dels conceptes bàsics d'XML, en particular l'ús de `<`, `</`, `>` i altres elements.

### 1. **Elements**
Els elements en XML estan delimitats per etiquetes d'obertura i tancament, on l'etiqueta d'obertura és `<element>` i l'etiqueta de tancament és `</element>`. Un element pot contenir dades o altres elements.

**Exemple d'un element:**
```xml
<nom>Pit de pollastre</nom>
```

En aquest exemple, `nom` és l'element que conté el valor `Pit de pollastre`.

### 2. **Atributs**
Els elements poden tenir atributs que proporcionen informació addicional. Els atributs es defineixen dins de l'etiqueta d'obertura i tenen el format clau-valor.

**Exemple d'un element amb atributs:**
```
<llibre idioma="català">El Petit Príncep</llibre>
```

En aquest exemple, `idioma` és un atribut amb el valor `català`, i l'element conté el text `El Petit Príncep`.

### 3. **Estructura en arbre**
XML té una estructura jeràrquica en forma d'arbre, on un element pot contenir altres elements "fills". Aquesta estructura és autodescriptiva, ja que cada element descriu el tipus de dades que conté.

**Exemple d'una estructura en arbre:**
<llibreria>
  <llibre>
    <títol>El Petit Príncep</títol>
    <autor>Antoine de Saint-Exupéry</autor>
    <any>1943</any>
  </llibre>
</llibreria>

En aquest exemple:
- `llibreria` és l'element "pare".
- `llibre` és un element "fill" de `llibreria`.
- Els elements `títol`, `autor` i `any` són fills de `llibre`.

### 4. **Regles sintàctiques**
- Tots els elements han de tenir una etiqueta d'obertura i una de tancament (`<element></element>`).
- Els noms dels elements són sensibles a majúscules i minúscules (`<Nom>` és diferent de `<nom>`).
- Els atributs han d'anar entre cometes dobles.
- Un document XML ha de tenir un únic element arrel (l'element que conté tots els altres elements).

---

**Exemple complet d'un document XML:**
```xml
<llibreria>
  <llibre isbn="3423423432">
    <títol>El Petit Príncep</títol>
    <autor>Antoine de Saint-Exupéry</autor>
    <any>1943</any>
  </llibre>
  <llibre isbn="343432888">
    <títol>1984</títol>
    <autor>George Orwell</autor>
    <any>1949</any>
  </llibre>
</llibreria>
```

En aquest exemple:
- `llibreria` és l'element arrel que conté dos elements `llibre`.
- Cada element `llibre` conté informació sobre un llibre, incloent el títol, l'autor i l'any de publicació.

Amb aquests conceptes, pots estructurar i gestionar informació utilitzant XML de manera organitzada i clara.


## Pràctica: Creació i validació d'un document XML

Objectiu: Aprendre a estructurar informació en un document XML i validar que la sintàxi és correcte.


Es vol emmagatzemar informació sobre libres en un document xml. La informació a emmagatzemar és.

* Títol, ISBN i categoria
* Autor
* Any de publicació
* Gènere

Un exemple d'xml és aquest:

```xml
<llibreria>
  <llibre isbn="3423423432" categoria="aventures">
    <títol>El Petit Príncep</títol>
    <autor>Antoine de Saint-Exupéry</autor>
    <any>1943</any>
  </llibre>
  <llibre isbn="343432888" categoria="distopies">
    <títol>1984</títol>
    <autor>George Orwell</autor>
    <any>1949</any>
  </llibre>
</llibreria>
```

Fes ara tu un fitxer xml que contingui informació sobre manjars:

* **Nom** i **categoria** (Exemple: Pit de pollastre, categoria carn)
* **Kilocalories** per 100 grams (Ex: 100)
* **Proteines** per 100 grams (Ex: 20)
* **Greixos** per 100 grams (Ex: 10)

Comprova que el teu document té un format correcte, per exemple a [XMLValidation](https://www.xmlvalidation.com/)

__Nota: si veus que es correcte, prova errors per tal que sigui incorrecte i vegis com el validador t'avisa que no és correcte__