# Sistemes de gestió empresarials

## Resultats d'aprenentatge i Continguts

### Resultats d'aprenentatge

**RA7.** Efectua operacions amb sistemes empresarials de gestió d'informació realitzant tasques d'importació, integració, assegurament i extracció de la informació.
   * 7.1. Identifica els principals sistemes de gestió empresarial.
   * 7.2. Reconeix els avantatges dels sistemes de gestió d'informació * empresarials.
   * 7.3. Avalua les característiques de les aplicacions de gestió empresarial * principals.
   * 7.4. Instal·la aplicacions de gestió de la informació empresarial.
   * 7.5. Configura i administra les aplicacions.
   * 7.6. Estableix i verifica mecanismes d'accés segur a la informació.
   * 7.7. Genera informes.
   * 7.8. Realitza procediments d'extracció d'informació per al tractament i * la incorporació a diversos sistemes.
   * 7.9. Elabora documents relatius a l'explotació de l'aplicació.

### Continguts

**Sistemes de gestió empresarial**
   * 7.1. Aplicacions de gestió empresarial. Tipus. Característiques.
   * 7.2. Instal·lació.
   * 7.3. Administració i configuració.
   * 7.4. Integració de mòduls.
   * 7.5. Mecanismes d'accés segur a la informació. Rols i privilegis.
   * 7.6. Elaboració d'informes.
   * 7.7. Exportació d'informació.

## Teoria

* Què és un ERP.
* ERP de codi lliure vs codi propietari.
* Quins mòduls contempla un ERP.
* Odoo com exemple de ERP.

## Pràctica

Farem una pràctica amb [Odoo](https://www.odoo.com/ca_ES)

>Odoo és un conjunt d'aplicacions empresarials de codi obert que cobreix totes les necessitats de la teva empresa: CRM, comerç electrònic, comptabilitat, inventari, punt de venda, gestió de projectes, etc.
>
>La proposta única de valor d'Odoo és ser molt fàcil d'utilitzar i estar totalment integrat, ambdues alhora.

Instal·laren [Odoo amb Docker](https://hub.docker.com/_/odoo). Cal engegar dos dockers: el Docker de la base de dades i el docker d'Odoo

```bash
docker run -d -e POSTGRES_USER=odoo -e POSTGRES_PASSWORD=odoo -e POSTGRES_DB=postgres --name db postgres:15
docker run -p 8069:8069 --name odoo --link db:db -t odoo
```

Per engegar i aturar:

```bash
docker stop odoo
docker start -a odoo
```

En que consistirà la pràctica:

* Farem grups d'entre 2 i 6 persones. Cada grup triarà un mòdul o mòduls d'Odoo que vulguin treballar. La pràctica consistirà en:
   * Instal·lar el/s mòdul/s triats.
   * Apendre a fer anar els mòduls triats.

* Entrebagles:
   * Captures de pantalla (o vídeos) on es vegi com l'alumnat ha fet la instal·lació de l'Odoo a la seva màquina.
   * Captures de pantalla (o vídeos) on es vegi com l'alumnat utilitza els mòduls que ha triat, amb la seva respectiva explicació. S'entregarà en format pdf (amb enllaços a vídeos si n'hi ha)
   * [Opcional] Presentació a la classe de com es fan servir els mòduls.
   * Tot s'entrega en pdf al Moodle. A la portada han d'aparèixer el nom de tots els alumnes del grup. Tothom ho ha d'entregar.

* Avaluació:
   * Per treure el 100% de la nota cal fer la presentació.
   * Es valorarà la capacitat que hagi assolit l'alumne per explicar els mòduls que ha provat.
   * Es valorarà la documentació entregada.
   * Es tindrà en compte el nombre d'alumnes del grup.
