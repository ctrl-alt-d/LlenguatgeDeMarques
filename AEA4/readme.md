# Persistència

Anem a estudiar la persistència usant llenguatge de marques. Per fer això aprendrem a *serialitzar* objectes a un llenguatge de marques i desar-ho a disc i aprendrem a *deserialitzar* des de llenguatge de marques per tal d' 'hidratar' objectes.

## Serialització en JSON

Per fer aquesta pràctica el que farem serà crear una sèrie de classes c#, instanciar-les amb valors i, finalment, persistir l'estat d'aquests objectes a disc en un format de llenguatge de marques JSON

Usarem l'[exemple de Microsoft](https://learn.microsoft.com/en-us/dotnet/standard/serialization/system-text-json/how-to#serialization-examples) per a fer la pràctica:


```c#
using System.Text.Json;

namespace SerializeBasic
{
    public class WeatherForecast
    {
        public DateTimeOffset Date { get; set; }
        public int TemperatureCelsius { get; set; }
        public string? Summary { get; set; }
    }

    public class Program
    {
        public static void Main()
        {
            var weatherForecast = new WeatherForecast
            {
                Date = DateTime.Parse("2019-08-01"),
                TemperatureCelsius = 25,
                Summary = "Hot"
            };

            string jsonString = JsonSerializer.Serialize(weatherForecast);

            Console.WriteLine(jsonString);
        }
    }
}
// output:
//{"Date":"2019-08-01T00:00:00-07:00","TemperatureCelsius":25,"Summary":"Hot"}
```

Si ens fixem a l'exemple crea en memòria un objecte de tipus `WeatherForecast`, la transforma a JSON i la mostra per consola.

Per tal de **persistir-ho** a disc cal usar el segon exemple:

```c#
using System.Text.Json;

namespace SerializeToFile
{
    public class WeatherForecast
    {
        public DateTimeOffset Date { get; set; }
        public int TemperatureCelsius { get; set; }
        public string? Summary { get; set; }
    }

    public class Program
    {
        public static void Main()
        {
            var weatherForecast = new WeatherForecast
            {
                Date = DateTime.Parse("2019-08-01"),
                TemperatureCelsius = 25,
                Summary = "Hot"
            };

            string fileName = "WeatherForecast.json"; 
            string jsonString = JsonSerializer.Serialize(weatherForecast);
            File.WriteAllText(fileName, jsonString);

            Console.WriteLine(File.ReadAllText(fileName));
        }
    }
}
// output:
//{"Date":"2019-08-01T00:00:00-07:00","TemperatureCelsius":25,"Summary":"Hot"}
```

Busca el fitxer que s'ha creat al sistema de fitxers. Obra'l amb VSCode, amb el Navegador o amb alguna altra aplicació i contesta:
* Hi ha tota la informació de l'objecte?
* Té format? (És a dir, està indentat i és de bon llegit o bé no té format i està tot seguit)

Mira la [documentació de Microsoft](https://learn.microsoft.com/en-us/dotnet/standard/serialization/system-text-json/how-to#serialize-to-formatted-json) i mira de serialitzar amb format.


Exercicis:
* Prepara en memòria una estructura més complexa que no pas la que hem fet servir a l'exemple. Aquesta estructura contindrà llistes d'objectes i dicionaris. Serialitza la teva estructura.

## Deserialització en JSON

Deserialitzar és el procés contrari a serialitzar. De manera ideal, podem tenir les classes c# preparades per deserialitzar un JSON. Quan el deserialitzem haurem d'informar al deserialitzador de quina és la classe que deserialitzem.

Treballem amb la [documentació de Microsoft de deserialització](https://learn.microsoft.com/en-us/dotnet/standard/serialization/system-text-json/deserialization#examples):

```c#
using System.Text.Json;

namespace DeserializeExtra
{
    public class WeatherForecast
    {
        public DateTimeOffset Date { get; set; }
        public int TemperatureCelsius { get; set; }
        public string? Summary { get; set; }
        public string? SummaryField;
        public IList<DateTimeOffset>? DatesAvailable { get; set; }
        public Dictionary<string, HighLowTemps>? TemperatureRanges { get; set; }
        public string[]? SummaryWords { get; set; }
    }

    public class HighLowTemps
    {
        public int High { get; set; }
        public int Low { get; set; }
    }

    public class Program
    {
        public static void Main()
        {
            string jsonString =
                """
                {
                  "Date": "2019-08-01T00:00:00-07:00",
                  "TemperatureCelsius": 25,
                  "Summary": "Hot",
                  "DatesAvailable": [
                    "2019-08-01T00:00:00-07:00",
                    "2019-08-02T00:00:00-07:00"
                  ],
                  "TemperatureRanges": {
                                "Cold": {
                                    "High": 20,
                      "Low": -10
                                },
                    "Hot": {
                                    "High": 60,
                      "Low": 20
                    }
                            },
                  "SummaryWords": [
                    "Cool",
                    "Windy",
                    "Humid"
                  ]
                }
                """;
                
            WeatherForecast? weatherForecast = 
                JsonSerializer.Deserialize<WeatherForecast>(jsonString);

            Console.WriteLine($"Date: {weatherForecast?.Date}");
            Console.WriteLine($"TemperatureCelsius: {weatherForecast?.TemperatureCelsius}");
            Console.WriteLine($"Summary: {weatherForecast?.Summary}");
        }
    }
}
// output:
//Date: 8/1/2019 12:00:00 AM -07:00
//TemperatureCelsius: 25
//Summary: Hot
```

A l'exemple es veu com deserialitzem un `string` i obtenim un objecte. En aquesta línia es veu com informem al deserialitzador del tipus de dades que estem deserialitzant: `JsonSerializer.Deserialize<WeatherForecast>(jsonString)`

Nosaltre volem deserialitzar JSON que estiguin persistits a disc. Llavors, observem el segon exemple, on podem veure com primer llegeix el JSON de disc:

```c#
using System.Text.Json;

namespace DeserializeFromFile
{
    public class WeatherForecast
    {
        public DateTimeOffset Date { get; set; }
        public int TemperatureCelsius { get; set; }
        public string? Summary { get; set; }
    }

    public class Program
    {
        public static void Main()
        {
            string fileName = "WeatherForecast.json";
            string jsonString = File.ReadAllText(fileName);
            WeatherForecast weatherForecast = JsonSerializer.Deserialize<WeatherForecast>(jsonString)!;

            Console.WriteLine($"Date: {weatherForecast.Date}");
            Console.WriteLine($"TemperatureCelsius: {weatherForecast.TemperatureCelsius}");
            Console.WriteLine($"Summary: {weatherForecast.Summary}");
        }
    }
}
// output:
//Date: 8/1/2019 12:00:00 AM -07:00
//TemperatureCelsius: 25
//Summary: Hot
```

Exercicis:

* Crea les classes c# per deserialitzar el següent JSON i deserialitza'l:

```json
{
  "factures": [
    {
      "id_factura": 1,
      "data": "2024-01-15",
      "client": {
        "id_client": 101,
        "nom": "Empresa XYZ",
        "adreça": "Carrer Major, 123, Barcelona"
      },
      "total": 250.75,
      "linies_factura": [
        {
          "id_linia": 1,
          "descripcio": "Producte A",
          "quantitat": 2,
          "preu_unitari": 50.00,
          "total_linia": 100.00
        },
        {
          "id_linia": 2,
          "descripcio": "Producte B",
          "quantitat": 3,
          "preu_unitari": 30.25,
          "total_linia": 90.75
        },
        {
          "id_linia": 3,
          "descripcio": "Descompte especial",
          "quantitat": 1,
          "preu_unitari": -10.00,
          "total_linia": -10.00
        }
      ]
    },
    {
      "id_factura": 2,
      "data": "2024-01-20",
      "client": {
        "id_client": 102,
        "nom": "Client ABC",
        "adreça": "Avinguda Central, 45, Madrid"
      },
      "total": 180.00,
      "linies_factura": [
        {
          "id_linia": 1,
          "descripcio": "Servei de consultoria",
          "quantitat": 1,
          "preu_unitari": 150.00,
          "total_linia": 150.00
        },
        {
          "id_linia": 2,
          "descripcio": "Producte C",
          "quantitat": 1,
          "preu_unitari": 30.00,
          "total_linia": 30.00
        }
      ]
    }
  ]
}
```

