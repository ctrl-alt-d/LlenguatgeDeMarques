# Pràctica: Ús d’un ERP amb Odoo

## Objectius

Aquesta pràctica té com a finalitat conèixer de primera mà el funcionament d’un sistema de gestió empresarial (ERP) mitjançant la instal·lació i ús de **Odoo**, un ERP de codi obert. L’alumnat experimentarà amb diversos mòduls d’Odoo per entendre el seu funcionament i veure com poden ajudar en la gestió d’una empresa.

---

## Requisits previs

- Tenir Docker instal·lat a l’ordinador.
- Coneixements bàsics d’ús de línia de comandes.
- Navegador web per accedir a Odoo.

---

## Instal·lació d’Odoo amb Docker

1. Engegar un contenidor per a la base de dades PostgreSQL:

```bash
docker run -d -e POSTGRES_USER=odoo -e POSTGRES_PASSWORD=odoo -e POSTGRES_DB=postgres --name db postgres:15
```

Nota: Si has fet el mòdul professional de base de dades, potser tindràs curiositat per veure les taules que crea **Odoo**. Per poder-te connectar amb **DBeaver** (o un altre client de base de dades) a aquest **PostgreSQL**, cal que publiquis el **port 5432** del contenidor, cosa que pots fer afegint el paràmetre `-p 5432:5432` com es mostra a la comanda anterior. Això et permetrà accedir a la base de dades des del teu ordinador com si fos un servidor local.


2. Engegar un contenidor per a Odoo:

```bash
docker run -p 8069:8069 --name odoo --link db:db -t odoo
```

3. Accedir a Odoo des del navegador:

```
http://localhost:8069
```

4. Crear una nova base de dades i configurar l’entorn d’administració.

### Per aturar i reiniciar:

**Aturar Odoo:**
```bash
docker stop odoo
```

**Reiniciar Odoo:**
```bash
docker start -a odoo
```

---

## Desenvolupament de la pràctica

1. **Formació de grups:** Els alumnes es dividiran en grups de 2 a 6 persones.

2. **Selecció de mòduls:** Cada grup triarà un o més mòduls d’Odoo per instal·lar i provar (ex: CRM, Vendes, Inventari, Comptabilitat...).

3. **Activitats a realitzar pel grup:**
   - Instal·lar els mòduls seleccionats.
   - Aprendre el seu funcionament mitjançant casos pràctics: crear clients, gestionar comandes, introduir productes, etc.
   - Documentar el procés amb captures de pantalla o vídeos.

---

## Lliurament

El treball es lliurarà en format PDF al Moodle. El document ha d’incloure:

- **Portada:** amb els noms complets de tots els integrants del grup.
- **Instal·lació d’Odoo:** captures o vídeos on es vegi el procés d’instal·lació. Reflexió sobre els avantatges de distribuir programari mitjançant Docker.
- **Ús dels mòduls:** demostració del funcionament dels mòduls triats, amb explicacions clares.
- **[Opcional] Presentació oral:** exposició a classe de com s’utilitzen els mòduls.

---

## Criteris d’avaluació

- **Instal·lació correcta de l’entorn i dels mòduls.**
- **Capacitat per entendre i explicar el funcionament dels mòduls.**
- **Qualitat de la documentació entregada.**
- **Presentació oral (opcional però necessària per obtenir el 100% de la nota).**
- **Nombre d’alumnes per grup (s’adaptarà el nivell d’exigència).**

---

## Recursos útils

- [Odoo oficial](https://www.odoo.com/ca_ES)
- [Docker Hub d’Odoo](https://hub.docker.com/_/odoo)
- [Documentació d’Odoo](https://www.odoo.com/documentation)

