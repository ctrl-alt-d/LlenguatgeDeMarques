## Sessió 7: Model de Caixa de CSS (Box Model)

### Objectius
- Entendre com funciona el model de caixa en CSS.
- Aplicar marges, farcits, i dimensions als elements.

### Continguts

#### 1. El Model de Caixa
Tots els elements HTML es representen com a caixes que consten de diverses capes. Aquestes capes inclouen:
- **Contingut (Content)**: L'àrea on es mostra el contingut, com el text o les imatges.
- **Farcit (Padding)**: L'espai entre el contingut i la vora de la caixa.
- **Contorn (Border)**: Un contorn que envolta el farcit (si està definit).
- **Marge (Margin)**: L'espai fora del contorn que separa l'element d'altres elements.

---

#### 2. Propietats Principals del Model de Caixa

**a. `margin`**
- Defineix l'espai exterior de la caixa (fora del contorn).
- **Exemples**:
  - margin: 20px; (defineix un marge de 20 píxels a tots els costats)
  - margin-top: 10px; (marge superior)
  - margin-right: 15px; (marge dret)
  - margin-bottom: 10px; (marge inferior)
  - margin-left: 5px; (marge esquerre)

**b. `padding`**
- Defineix l'espai interior de la caixa (entre el contingut i el contorn).
- **Exemples**:
  - padding: 15px; (defineix un farcit de 15 píxels a tots els costats)
  - padding-top: 5px; (farcit superior)
  - padding-right: 10px; (farcit dret)
  - padding-bottom: 5px; (farcit inferior)
  - padding-left: 10px; (farcit esquerre)

**c. `border`**
- Defineix un contorn al voltant de l'element.
- **Exemples**:
  - border: 2px solid #000; (un contorn de 2 píxels, línia contínua, color negre)
  - border-top: 1px dashed #ccc; (contorn superior de línia discontínua)
  - border-radius: 10px; (fa les vores arrodonides)

**d. `width` i `height`**
- Defineixen l'ample i l'altura del contingut de la caixa (no inclouen marges, farcits ni contorns).
- **Exemples**:
  - width: 100px; (ample de 100 píxels)
  - height: 200px; (altura de 200 píxels)

---

#### 3. Diferència entre Marges, Farcits i Contorns
- **Marge (Margin)**: Espai fora de la caixa que separa l'element d'altres elements.
- **Farcit (Padding)**: Espai dins de la caixa que separa el contingut del contorn.
- **Contorn (Border)**: Línia que envolta el farcit i defineix els límits de la caixa.

---

## Esquema en ASCII del Model de Caixa

Aquest esquema mostra la disposició del `margin`, `border`, `padding` i `content` en una caixa CSS.

```plaintext
+-----------------------------+
|         MARGIN              |
|  +------------------------+ |
|  |       BORDER           | |
|  |  +-------------------+ | |
|  |  |     PADDING       | | |
|  |  |  +-------------+  | | |
|  |  |  |  CONTENT    |  | | |
|  |  |  +-------------+  | | |
|  |  +-------------------+ | |
|  +------------------------+ |
+-----------------------------+
```

### Descripció
- **MARGIN**: Espai exterior que envolta el contorn de la caixa.
- **BORDER**: Contorn que envolta el farcit de la caixa.
- **PADDING**: Espai entre el contingut i el contorn.
- **CONTENT**: L'àrea on es mostra el contingut, com text o imatges.

---

Més informació a w3schools: [CSS Box Model](https://www.w3schools.com/css/css_boxmodel.asp)

### Exercicis Pràctics
1. **Exercici 1**: Defineix una caixa amb un contorn de 2 píxels, un farcit de 10 píxels i un marge de 20 píxels.
2. **Exercici 2**: Experimenta canviant les propietats de `margin` i `padding` per veure com afecten la disposició dels elements.
3. **Exercici 3**: Fes servir `border-radius` per crear una caixa amb les cantonades arrodonides.


## Exercicis per calcular l'amplada total

### Exercici 1
Aquest `<div>` tindrà una amplada total de 260px i una altura total de 130px:

div {
  width: 200px;
  height: 100px;
  padding: 15px;
  border: 5px solid black;
  margin: 0;
}

**Càlcul de l'amplada:**
  200px (amplada de l'àrea de contingut)
+ 30px (padding esquerre + padding dret: 15px + 15px)
+ 10px (contorn esquerre + contorn dret: 5px + 5px)
= 260px (amplada total)

**Càlcul de l'altura:**
  100px (altura de l'àrea de contingut)
+ 30px (padding superior + padding inferior: 15px + 15px)
+ 10px (contorn superior + contorn inferior: 5px + 5px)
= 130px (altura total)

---

### Exercici 2
Aquest `<div>` tindrà una amplada total de 400px i una altura total de 120px:

div {
  width: 350px;
  height: 80px;
  padding: 20px;
  border: 5px solid blue;
  margin: 0;
}

**Càlcul de l'amplada:**
  350px (amplada de l'àrea de contingut)
+ 40px (padding esquerre + padding dret: 20px + 20px)
+ 10px (contorn esquerre + contorn dret: 5px + 5px)
= 400px (amplada total)

**Càlcul de l'altura:**
  80px (altura de l'àrea de contingut)
+ 40px (padding superior + padding inferior: 20px + 20px)
+ 10px (contorn superior + contorn inferior: 5px + 5px)
= 120px (altura total)

---

### Exercici 3
Aquest `<div>` tindrà una amplada total de 500px i una altura total de 250px:

div {
  width: 450px;
  height: 200px;
  padding: 25px;
  border: 0;
  margin: 0;
}

**Càlcul de l'amplada:**
  Completa tu mateix, t'ha de sortir 500px (amplada total)

**Càlcul de l'altura:**
  Completa tu mateix, t'ha de sortir 250px (altura total)
