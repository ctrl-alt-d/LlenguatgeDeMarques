# Pràctica 1

## Observa aquest codi c#

```c#
using System;
using System.Xml.Serialization;
using System.Collections.Generic;

[XmlRoot("Persona")]
public class Persona
{
    [XmlAttribute("Id")]
    public int Id { get; set; }

    [XmlElement("Nom")]
    public string Nom { get; set; } = default!;

    [XmlElement("Edat")]
    public int Edat { get; set; }

    [XmlArray("Mascotes")]
    [XmlArrayItem("Mascota")]
    public List<Mascota> Mascotes { get; set; } = new();
}

public class Mascota
{
    [XmlAttribute("Nom")]
    public string Nom { get; set; } = default!;

    [XmlElement("Tipus")]
    public string Tipus { get; set; } = default!;
}


class Programa
{
    static void Main(string[] args)
    {
        var persona = new Persona
        {
            Id = 1,
            Nom = "Laura",
            Edat = 30,
            Mascotes = new List<Mascota>
            {
                new() { Nom = "Nina", Tipus = "Gos" },
                new() { Nom = "Mimi", Tipus = "Gat" }
            }
        };

        string fitxer = "persona.xml";

        // SERIALITZAR
        XmlSerializer serializer = new(typeof(Persona));
        using (FileStream fs = new(fitxer, FileMode.Create))
        {
            serializer.Serialize(fs, persona);
        }

        Console.WriteLine("Fitxer XML creat!");

        // DESERIALITZAR
        using (FileStream fs = new(fitxer, FileMode.Open))
        {
            var personaDeserialitzada = (Persona)(
                serializer.Deserialize(fs) ?? 
                throw new InvalidOperationException("Deserialització fallida")
            );
            Console.WriteLine($"Persona: {personaDeserialitzada.Nom}, Edat: {personaDeserialitzada.Edat}");
            foreach (var m in personaDeserialitzada.Mascotes)
            {
                Console.WriteLine($" - Mascota: {m.Nom}, Tipus: {m.Tipus}");
            }
        }
    }
}
```

## Modifica el codi

Anem a modificar el codi anterior, el codi està tot al main i volem fer el programa més modular.

Observa aquesta la interfície de sota i fes una classe que la implementi.

Posa les classes `Persona` i `Mascota` cadascuna a un fitxer diferent (fora del `Program.cs`)

```c#
using System.Xml.Serialization;
using System.Collections.Generic;

public interface IOperacio
{
    /// <summary>
    /// Crea una persona, s'inventa les dades
    /// </summary>
    /// <returns>Una persona</returns>
    Persona GetPersonaFromRandom();

    /// <summary>
    /// Desar una persona a un fitxer XML
    /// </summary>
    /// <param name="fitxer">Nom del fitxer, sense extensió (la funció li posarà extensió XML)</param>
    /// <param name="persona">Dades a serialitzar</param>
    void DesarPersonaAsXml(string fitxer, Persona persona);

    /// <summary>
    /// Desar una persona a un fitxer JSON
    /// </summary>
    /// <param name="fitxer">Nom del fitxer, sense extensió (la funció li posarà extensió JSON)</param>
    /// <param name="persona">>Dades a serialitzar</param>
    void DesarPersonaAsJson(string fitxer, Persona persona);

    /// <summary>
    /// Obtenir una persona d'un fitxer XML
    /// </summary>
    /// <param name="fitxer">Nom del fitxer, sense extensió (la funció li posarà extensió XML)</param>
    /// <returns>Una persona</returns>
    Persona GetPersonaFromXml(string fitxer);

    /// <summary>
    ///  Obtenir una persona d'un fitxer JSON
    /// </summary>
    /// <param name="fitxer">>Nom del fitxer, sense extensió (la funció li posarà extensió JSON)</param>
    /// <returns>Una persona</returns>
    Persona GetPersonaFromJson(string fitxer);

    /// <summary>
    /// Imprimir per consola les dades d'una persona
    /// </summary>
    /// <param name="persona">>Persona a imprimir</param>
    void PintaPersonaPerConsola(Persona persona);
}
```

Ara anem a modificar el Main. Instànciarem la classe que has creat i crearem a dins dues variables més, una variable per emmagatzemar `Persona` (inicialment inicialitzada amb `GetPersonaFromRandom()`) i una variable on posar el nom del fitxer on serialitzem, inicialment `persona`.

Ara crea un menú que anirà preguntant a l'usuari què vol fer:

```
0) Sortir
1) Desar persona com XML
2) Desar persona com JSON
3) Llegir persona des d'XML
4) Llegir persona des de JSON
5) Definir nom de fitxer
9) Pintar dades
```

## Entregables de la pràctica:

* Cal entregar un pdf amb el codi del programa i exemples del programa en funcionament. Captura de pantalla de les dades exportades a JSON.
* Volem canviar ara el nom de la propietat `Nom` de `Persona`, ara volem que sigui `NomCognoms`. Podem canviar-lo i seguir carregant els XML que ja tinguem sense probemes? Podem carregar els JSON? Com podem fer per poder carregar els JSON, sense tocar els JSON, si canviem el nom d'aquesta propietat? (Consulta [Use a custom JSON property naming policy](https://learn.microsoft.com/en-us/dotnet/standard/serialization/system-text-json/customize-properties#customize-individual-property-names))