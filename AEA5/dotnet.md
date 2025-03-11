# Validar un xml contra el seu esquema

## xml:

```xml
<?xml version="1.0" encoding="utf-8"?>
<Persona>
  <Nombre>Juan Pérez</Nombre>
  <Edad>30</Edad>
</Persona>
```

## XSD

```xml
<?xml version="1.0" encoding="utf-8"?>
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema">
  <xs:element name="Persona">
    <xs:complexType>
      <xs:sequence>
        <xs:element name="Nombre" type="xs:string"/>
        <xs:element name="Edad" type="xs:int"/>
      </xs:sequence>
    </xs:complexType>
  </xs:element>
</xs:schema>
```

## C#


```c#
using System;
using System.IO;
using System.Xml;
using System.Xml.Schema;

class Program
{
    static void Main()
    {
        string xmlPath = "archivo.xml";  // Ruta del archivo XML
        string xsdPath = "archivo.xsd";  // Ruta del archivo XSD

        if (ValidateXml(xmlPath, xsdPath))
        {
            Console.WriteLine("✅ El XML es válido según el esquema XSD.");
        }
        else
        {
            Console.WriteLine("❌ El XML no es válido. Revisa los errores.");
        }
    }

    public static bool ValidateXml(string xmlFilePath, string xsdFilePath)
    {
        bool isValid = true;
        XmlSchemaSet schemaSet = new XmlSchemaSet();
        schemaSet.Add("", xsdFilePath);

        XmlReaderSettings settings = new XmlReaderSettings();
        settings.Schemas = schemaSet;
        settings.ValidationType = ValidationType.Schema;
        settings.ValidationEventHandler += (sender, args) =>
        {
            isValid = false;
            Console.WriteLine($"[ERROR] Línea {args.Exception.LineNumber}, Columna {args.Exception.LinePosition}: {args.Message}");
        };

        using (XmlReader reader = XmlReader.Create(xmlFilePath, settings))
        {
            try
            {
                while (reader.Read()) { } // Procesa todo el XML
            }
            catch (Exception ex)
            {
                isValid = false;
                Console.WriteLine($"[EXCEPCIÓN] {ex.Message}");
            }
        }

        return isValid;
    }
}
```
