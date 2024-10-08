# Sessió 3: Taules en HTML

**Objectius:**
1. Aprendre a crear taules i formularis en HTML.

---

## 1. Introducció a les Taules (30 min)
- **Etiqueta de taula (`<table>`):** Utilitzada per a crear una taula.
- **Files (`<tr>`):** Representen cada fila de la taula.
- **Cel·les de dades (`<td>`):** Contenen el contingut de cada cel·la de la taula.
- **Cel·les d'encapçalament (`<th>`):** Utilitzades per a definir les cel·les d'encapçalament de la taula, generalment en negreta i centrades.
  
**Exemple bàsic de taula:**

```html
<table>
  <tr>
    <th>Encapçalament 1</th>
    <th>Encapçalament 2</th>
  </tr>
  <tr>
    <td>Dada 1</td>
    <td>Dada 2</td>
  </tr>
  <tr>
    <td>Dada 3</td>
    <td>Dada 4</td>
  </tr>
</table>
```

---

## 2. Estructura avançada de Taules (30 min)
- **Encapçalament de taula (`<thead>`):** Utilitzat per a definir el conjunt de cel·les d'encapçalament.
- **Corps de taula (`<tbody>`):** Conté el contingut principal de la taula.

**Exemple de taula amb encapçalament i cos:**

```html
<table>
  <thead>
    <tr>
      <th>Nom</th>
      <th>Edats</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Ana</td>
      <td>25</td>
    </tr>
    <tr>
      <td>Joan</td>
      <td>30</td>
    </tr>
  </tbody>
</table>
```

---

## 3. Activitat pràctica
- Crear una taula que inclogui:
  - Un encapçalament amb dues cel·les.
  - Tres files de dades amb dues cel·les cadascuna.
  - Utilitzar les etiquetes `<thead>` i `<tbody>`.

---
