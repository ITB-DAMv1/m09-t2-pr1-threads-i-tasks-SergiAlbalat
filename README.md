[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/xs3aclQL)
### Repositori Part 1:
[Repositori](https://github.com/SergiAlbalat/T2.PR1.ThreadsTasks_SergiAlbalat)
### Repositori Part 2:
[Repositori](https://github.com/SergiAlbalat/T2.PR1.ThreadsTasksPart2.SergiAlbalt)

## Solució proposada:
En la part 1 he fet que els comensals bloquegin amb un lock els pals per que puguin utilizar els seus i despres al deixar-los el següents els agafi. En la segona solució per poder pintar, calcular i escoltar teclat he utilitzat Tasks que es troben en un bucle funcionant continuament. He deixat pujat un esquema dels dos enunciats en aquest repositori per poder veure la distribucio del funcionament de cada projecte.

## Dades analisi enunciat 1
- Comensals que han passat fam: 0
- Temps mitja de cada comensal: Aproximadament 3,1 segons
- Mitjana de vegades que cada consal ha menjat: 13
- Record de vegades que ha menjat un matei comensal: 14
- Record de menys vegades que ha menjat un comensal: 12

## Bibliografia

Eduard, E.(28/04/2025). T2.Processos. Documents de google. Recuperat el 06/05/2025 de [link](https://docs.google.com/document/d/1MtD84t79YI1Fm-wjA_nPslMbRfye_c0NplgustQXdSo/edit?tab=t.0#heading=h.ishb2r2lex5e)
Ediard, E.(06/05/2025). M09T2-Process. Github. Recuperat el 09/05/2025 de [link](https://github.com/eduard-ruesga-xtec/M09T2-Process)
📎 Si uso lock en .net para bloquear un objeto en un thread si otro thread quiere acceder al objeto se espera o no hace lo que hay en el lock?
> Cuando usas lock en .NET para bloquear un objeto en un hilo, cualquier otro hilo que intente acceder a ese objeto dentro de un bloque lock se quedará esperando hasta que el primer hilo libere el bloqueo.

Aquí hay un ejemplo simple:

csharp
class Program
{
    static object bloqueo = new object();

    static void MetodoSeguro()
    {
        lock (bloqueo)
        {
            Console.WriteLine($"{Thread.CurrentThread.ManagedThreadId} está dentro del lock");
            Thread.Sleep(2000); // Simula una operación prolongada
        }
    }

    static void Main()
    {
        Thread t1 = new Thread(MetodoSeguro);
        Thread t2 = new Thread(MetodoSeguro);

        t1.Start();
        t2.Start();

        t1.Join();
        t2.Join();
    }
}
En este código, ambos hilos intentan ejecutar MetodoSeguro(). El segundo hilo tendrá que esperar hasta que el primero salga del bloque lock, porque el objeto bloqueo está restringido por el primer hilo que lo adquirió.

Si tienes más preguntas sobre concurrencia en .NET, dime y seguimos explorando. 🚀
📎 Como usar append en csv writer en .net
> Para agregar datos a un archivo CSV en .NET, puedes usar StreamWriter con el parámetro append en true. También puedes utilizar la biblioteca CsvHelper para manejar CSV de manera más eficiente.

Aquí tienes un ejemplo con StreamWriter:

csharp
using System;
using System.IO;
using System.Globalization;
using CsvHelper;
using CsvHelper.Configuration;

class Program
{
    static void Main()
    {
        string filePath = "datos.csv";
        bool append = true;

        var config = new CsvConfiguration(CultureInfo.InvariantCulture)
        {
            HasHeaderRecord = !append // Evita escribir el encabezado si estás agregando datos
        };

        using (var writer = new StreamWriter(filePath, append))
        using (var csv = new CsvWriter(writer, config))
        {
            var records = new[]
            {
                new { Nombre = "Juan", Edad = 30 },
                new { Nombre = "Maria", Edad = 25 }
            };

            csv.WriteRecords(records);
        }

        Console.WriteLine("Datos agregados al archivo CSV.");
    }
}
Este código:

Usa StreamWriter(filePath, append) para agregar datos en lugar de sobrescribir el archivo.

Configura CsvHelper para omitir el encabezado si se está agregando información.

Escribe nuevos registros en el archivo CSV.

Si prefieres una solución más simple sin CsvHelper, puedes usar File.AppendAllText:

csharp
string filePath = "datos.csv";
string nuevoRegistro = "Carlos,40" + Environment.NewLine;
File.AppendAllText(filePath, nuevoRegistro);
Esto simplemente agrega una nueva línea al archivo CSV.

Si necesitas más detalles, puedes revisar este recurso sobre cómo manejar CSV en C#. 🚀
📎 Como puedo cambiar el tamaño de la consola en .net
> Para cambiar el tamaño de la consola en .NET, puedes usar la clase Console con Console.SetWindowSize(ancho, alto). Aquí tienes un ejemplo:

csharp
using System;

class Program
{
    static void Main()
    {
        Console.SetWindowSize(100, 30); // Cambia el tamaño de la ventana de la consola
        Console.WriteLine("Tamaño de consola cambiado!");
    }
}
🔹 SetWindowSize(ancho, alto) ajusta la ventana de la consola a los valores que especifiques. 🔹 SetBufferSize(ancho, alto) cambia el tamaño del búfer de la consola, útil si necesitas más espacio sin alterar la ventana visible. 🔹 Advertencia: en algunos sistemas operativos o configuraciones de consola, SetWindowSize puede lanzar una excepción si la ventana no permite ajustes. Usa try-catch para manejar esto.

Si necesitas más personalización, dime qué buscas exactamente. 🚀
