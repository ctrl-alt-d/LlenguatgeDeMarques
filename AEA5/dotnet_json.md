# Validar un jsnon contra el seu esquema

Nota, les llibreries dotnet encara no suporten validació d'esquema, s'ha fet servir https://www.nuget.org/packages/JsonSchema.Net/

> `dotnet add package JsonSchema.Net`

## json:

```json
{
  "Persona": {
    "Nombre": "Juan Pérez",
    "Edad": 30
  }
}
```

## XSD

```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "type": "object",
  "properties": {
    "Persona": {
      "type": "object",
      "properties": {
        "Nombre": { "type": "string" },
        "Edad": { "type": "integer" }
      },
      "required": ["Nombre", "Edad"]
    }
  },
  "required": ["Persona"]
}

```

## C#


```c#
using System;
using System.IO;
using Newtonsoft.Json;
using Newtonsoft.Json.Linq;
using Newtonsoft.Json.Schema;

class Program
{
    static void Main()
    {
        string jsonPath = "archivo.json";  // Ruta del fitxer JSON
        string schemaPath = "esquema.json";  // Ruta del fitxer JSON Schema

        if (ValidateJson(jsonPath, schemaPath))
        {
            Console.WriteLine("✅ El JSON és vàlid segons l'esquema JSON Schema.");
        }
        else
        {
            Console.WriteLine("❌ El JSON no és vàlid. Revisa els errors.");
        }
    }

    public static bool ValidateJson(string jsonFilePath, string schemaFilePath)
    {
        // Variable per indicar si el JSON és vàlid o no
        bool isValid = true;

        try
        {
            // Llegeix el fitxer JSON i el fitxer de l'esquema
            string jsonText = File.ReadAllText(jsonFilePath);
            string schemaText = File.ReadAllText(schemaFilePath);

            // Converteix l'esquema JSON a un objecte JSchema
            JSchema schema = JSchema.Parse(schemaText);

            // Converteix el JSON a un objecte JObject
            JObject jsonObject = JObject.Parse(jsonText);

            // Llista per a emmagatzemar errors de validació
            IList<string> errors = new List<string>();

            // Valida el JSON contra l'esquema
            if (!jsonObject.IsValid(schema, out errors))
            {
                isValid = false;
                Console.WriteLine("[ERRORS DE VALIDACIÓ]");
            }
        }
        catch (Exception ex)
        {
            isValid = false;
            Console.WriteLine($"[EXCEPCIÓ] {ex.Message}");
        }

        return isValid;
    }
}
```
