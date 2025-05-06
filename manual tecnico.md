# Manual Técnico - AutoGest Pro

## Índice
1. [Introducción](#introducción)
2. [Arquitectura del Sistema](#arquitectura-del-sistema)
   - [Diagrama de Componentes](#diagrama-de-componentes)
   - [Patrón de Diseño](#patrón-de-diseño)
3. [Estructuras de Datos Implementadas](#estructuras-de-datos-implementadas)
   - [Lista Doblemente Enlazada](#lista-doblemente-enlazada)
   - [Árbol AVL](#árbol-avl)
   - [Árbol Binario](#árbol-binario)
   - [Blockchain](#blockchain)
   - [Grafo No Dirigido](#grafo-no-dirigido)
   - [Compresión Huffman](#compresión-huffman)
   - [Árbol de Merkle](#árbol-de-merkle)
4. [Clases y Componentes Principales](#clases-y-componentes-principales)
   - [Usuarios](#usuarios)
   - [Vehículos](#vehículos)
   - [Repuestos](#repuestos)
   - [Servicios](#servicios)
   - [Facturas](#facturas)
5. [Algoritmos Principales](#algoritmos-principales)
   - [Algoritmo de Blockchain](#algoritmo-de-blockchain)
   - [Algoritmo de Huffman](#algoritmo-de-huffman)
   - [Recorridos en Árboles](#recorridos-en-árboles)
   - [Algoritmo de Árbol de Merkle](#algoritmo-de-árbol-de-merkle)
6. [Interfaz Gráfica](#interfaz-gráfica)
   - [Componentes GTK](#componentes-gtk)
   - [Diseño de Ventanas](#diseño-de-ventanas)
7. [Manejo de Archivos](#manejo-de-archivos)
   - [Carga y Lectura de JSON](#carga-y-lectura-de-json)
   - [Generación de Archivos de Backup](#generación-de-archivos-de-backup)
8. [Reportes con Graphviz](#reportes-con-graphviz)
   - [Generación de DOT](#generación-de-dot)
   - [Conversión a Imágenes](#conversión-a-imágenes)
9. [Compilación y Ejecución](#compilación-y-ejecución)
   - [Requisitos Previos](#requisitos-previos)
   - [Proceso de Compilación](#proceso-de-compilación)
   - [Directivas de Ejecución](#directivas-de-ejecución)
10. [Consideraciones de Seguridad](#consideraciones-de-seguridad)
    - [Encriptación de Contraseñas](#encriptación-de-contraseñas)
    - [Validación de Datos](#validación-de-datos)
11. [Pruebas Unitarias](#pruebas-unitarias)
    - [Casos de Prueba](#casos-de-prueba)
12. [Depuración y Solución de Problemas](#depuración-y-solución-de-problemas)
13. [Referencias](#referencias)

## Introducción

Este manual técnico describe la implementación y el funcionamiento interno del sistema AutoGest Pro, una aplicación de gestión para talleres de reparación de vehículos. El documento está dirigido a desarrolladores, administradores de sistemas y personal técnico que necesite comprender la arquitectura, las estructuras de datos y los algoritmos utilizados en el sistema.

AutoGest Pro está desarrollado en C# utilizando la biblioteca GTK para la interfaz gráfica. El sistema implementa varias estructuras de datos avanzadas para garantizar eficiencia, seguridad e integridad en el manejo de la información.

## Arquitectura del Sistema

### Diagrama de Componentes

AutoGest Pro sigue una arquitectura de múltiples capas para separar la lógica de presentación, la lógica de negocio y el acceso a datos. A continuación se muestra el diagrama de componentes del sistema:

![Diagrama de componentes]

### Patrón de Diseño

El sistema utiliza principalmente el patrón de diseño MVC (Modelo-Vista-Controlador) para separar la lógica de la aplicación:

1. **Modelo**: Contiene las clases que representan las entidades del sistema (Usuarios, Vehículos, Repuestos, Servicios, Facturas) y las estructuras de datos (Blockchain, Árbol AVL, etc.).
2. **Vista**: Implementada con GTK, maneja la presentación y la interacción con el usuario.
3. **Controlador**: Coordina las acciones del usuario, manipula el modelo y actualiza la vista.

Adicionalmente, se utilizan otros patrones como:
- **Singleton**: Para estructuras únicas como el Blockchain
- **Factory**: Para la creación de diferentes tipos de reportes
- **Observer**: Para la actualización de la interfaz cuando cambian los datos

## Estructuras de Datos Implementadas

### Lista Doblemente Enlazada

La lista doblemente enlazada se utiliza para almacenar los vehículos en el sistema. Su implementación consta de los siguientes elementos:

```csharp
public class NodoDoble<T>
{
    public T Valor { get; set; }
    public NodoDoble<T> Siguiente { get; set; }
    public NodoDoble<T> Anterior { get; set; }

    public NodoDoble(T valor)
    {
        Valor = valor;
        Siguiente = null;
        Anterior = null;
    }
}

public class ListaDoblementeEnlazada<T>
{
    private NodoDoble<T> cabeza;
    private NodoDoble<T> cola;
    public int Tamaño { get; private set; }

    public ListaDoblementeEnlazada()
    {
        cabeza = null;
        cola = null;
        Tamaño = 0;
    }

    // Métodos de inserción, eliminación, búsqueda, etc.
}
```

#### Complejidad Temporal:
- Inserción: O(1) en extremos, O(n) en posición intermedia
- Búsqueda: O(n)
- Eliminación: O(1) con referencia directa, O(n) por valor o posición

### Árbol AVL

El árbol AVL se implementa para gestionar los repuestos, garantizando un tiempo de búsqueda logarítmico. La implementación incluye rotaciones para mantener el equilibrio:

```csharp
public class NodoAVL<T> where T : IComparable<T>
{
    public T Valor { get; set; }
    public NodoAVL<T> Izquierdo { get; set; }
    public NodoAVL<T> Derecho { get; set; }
    public int Altura { get; set; }

    public NodoAVL(T valor)
    {
        Valor = valor;
        Izquierdo = null;
        Derecho = null;
        Altura = 1;
    }
}

public class ArbolAVL<T> where T : IComparable<T>
{
    private NodoAVL<T> raiz;

    public ArbolAVL()
    {
        raiz = null;
    }

    // Métodos de inserción, rotación, eliminación, búsqueda, etc.
}
```

#### Complejidad Temporal:
- Inserción: O(log n)
- Búsqueda: O(log n)
- Eliminación: O(log n)
- Rotaciones: O(1)

### Árbol Binario

Para la gestión de servicios se utiliza un árbol binario, permitiendo recorridos jerárquicos eficientes:

```csharp
public class NodoBinario<T> where T : IComparable<T>
{
    public T Valor { get; set; }
    public NodoBinario<T> Izquierdo { get; set; }
    public NodoBinario<T> Derecho { get; set; }

    public NodoBinario(T valor)
    {
        Valor = valor;
        Izquierdo = null;
        Derecho = null;
    }
}

public class ArbolBinario<T> where T : IComparable<T>
{
    private NodoBinario<T> raiz;

    public ArbolBinario()
    {
        raiz = null;
    }

    // Métodos de inserción, eliminación, búsqueda, recorridos, etc.
}
```

#### Complejidad Temporal:
- Inserción: O(n) en el peor caso, O(log n) promedio en árbol balanceado
- Búsqueda: O(n) en el peor caso, O(log n) promedio en árbol balanceado
- Recorridos: O(n)

### Blockchain

El Blockchain se implementa para almacenar de forma segura los usuarios del sistema. Cada bloque contiene información del usuario y está enlazado criptográficamente al bloque anterior:

```csharp
public class Bloque
{
    public int Index { get; set; }
    public string Timestamp { get; set; }
    public string Data { get; set; }
    public int Nonce { get; set; }
    public string PreviousHash { get; set; }
    public string Hash { get; set; }

    public Bloque(int index, string timestamp, string data, string previousHash)
    {
        Index = index;
        Timestamp = timestamp;
        Data = data;
        PreviousHash = previousHash;
        Nonce = 0;
        Hash = CalcularHash();
    }

    public string CalcularHash()
    {
        // Implementación del algoritmo SHA-256
    }

    public void MinarBloque(int dificultad)
    {
        // Implementación de la prueba de trabajo
    }
}

public class Blockchain
{
    private List<Bloque> cadena;
    private int dificultad;

    public Blockchain(int dificultad = 4)
    {
        this.dificultad = dificultad;
        cadena = new List<Bloque>();
        CrearBloqueGenesis();
    }

    private void CrearBloqueGenesis()
    {
        // Creación del bloque inicial
    }

    public void AgregarBloque(string data)
    {
        // Añadir un nuevo bloque a la cadena
    }

    public bool EsValida()
    {
        // Validación de la integridad de la cadena
    }
}
```

#### Complejidad Temporal:
- Creación de bloque: O(1)
- Minado de bloque: Variable (depende de la dificultad)
- Validación de cadena: O(n), donde n es el número de bloques

### Grafo No Dirigido

El grafo no dirigido se utiliza para modelar las relaciones entre vehículos y repuestos:

```csharp
public class NodoGrafo<T>
{
    public T Valor { get; set; }
    public List<NodoGrafo<T>> Adyacentes { get; set; }

    public NodoGrafo(T valor)
    {
        Valor = valor;
        Adyacentes = new List<NodoGrafo<T>>();
    }
}

public class GrafoNoDirigido<T>
{
    private Dictionary<T, NodoGrafo<T>> nodos;

    public GrafoNoDirigido()
    {
        nodos = new Dictionary<T, NodoGrafo<T>>();
    }

    public void AgregarNodo(T valor)
    {
        if (!nodos.ContainsKey(valor))
        {
            nodos.Add(valor, new NodoGrafo<T>(valor));
        }
    }

    public void AgregarArista(T origen, T destino)
    {
        // Verificar que los nodos existan
        AgregarNodo(origen);
        AgregarNodo(destino);

        // Añadir relación bidireccional
        nodos[origen].Adyacentes.Add(nodos[destino]);
        nodos[destino].Adyacentes.Add(nodos[origen]);
    }

    // Otros métodos: eliminación, búsqueda, recorridos, etc.
}
```

#### Complejidad Temporal:
- Agregar nodo: O(1)
- Agregar arista: O(1)
- Búsqueda de adyacencia: O(n), donde n es el número de adyacentes

### Compresión Huffman

El algoritmo de compresión Huffman se implementa para reducir el tamaño de los reportes:

```csharp
public class NodoHuffman : IComparable<NodoHuffman>
{
    public char? Caracter { get; }
    public int Frecuencia { get; }
    public NodoHuffman Izquierdo { get; }
    public NodoHuffman Derecho { get; }

    public NodoHuffman(char? caracter, int frecuencia, NodoHuffman izquierdo = null, NodoHuffman derecho = null)
    {
        Caracter = caracter;
        Frecuencia = frecuencia;
        Izquierdo = izquierdo;
        Derecho = derecho;
    }

    public bool EsHoja() => Izquierdo == null && Derecho == null;

    public int CompareTo(NodoHuffman otro) => Frecuencia.CompareTo(otro.Frecuencia);
}

public class CompresorHuffman
{
    public Dictionary<char, string> ConstruirTablaHuffman(string texto)
    {
        // Contar frecuencia de caracteres
        // Construir árbol de Huffman
        // Generar códigos para cada caracter
    }

    public string Comprimir(string texto)
    {
        // Implementación de la compresión
    }

    public string Descomprimir(string textoComprimido, Dictionary<char, string> tabla)
    {
        // Implementación de la descompresión
    }
}
```

#### Complejidad Temporal:
- Construcción del árbol: O(n log n), donde n es el número de caracteres únicos
- Compresión: O(n), donde n es la longitud del texto
- Descompresión: O(n), donde n es la longitud del texto comprimido

### Árbol de Merkle

El Árbol de Merkle se implementa para la gestión de facturas, garantizando la integridad de los datos:

```csharp
public class NodoMerkle
{
    public string Hash { get; set; }
    public NodoMerkle Izquierdo { get; set; }
    public NodoMerkle Derecho { get; set; }
    public string Data { get; set; }

    public NodoMerkle(string data)
    {
        Data = data;
        Hash = CalcularHash(data);
    }

    public NodoMerkle(NodoMerkle izquierdo, NodoMerkle derecho)
    {
        Izquierdo = izquierdo;
        Derecho = derecho;
        Hash = CalcularHash(izquierdo.Hash + derecho.Hash);
    }

    private string CalcularHash(string data)
    {
        // Implementación de SHA-256
    }
}

public class ArbolMerkle
{
    public NodoMerkle Raiz { get; private set; }
    private List<string> transacciones;

    public ArbolMerkle(List<string> transacciones)
    {
        this.transacciones = transacciones;
        ConstruirArbol();
    }

    private void ConstruirArbol()
    {
        // Implementación para construir el árbol desde las hojas hasta la raíz
    }

    public bool VerificarIntegridad(string transaccion, string hash, List<string> prueba)
    {
        // Implementación para verificar la integridad de una transacción
    }
}
```

#### Complejidad Temporal:
- Construcción del árbol: O(n), donde n es el número de transacciones
- Verificación de integridad: O(log n)

## Clases y Componentes Principales

### Usuarios

La clase Usuario representa a los clientes del taller y propietarios de los vehículos:

```csharp
public class Usuario
{
    public int ID { get; set; }
    public string Nombres { get; set; }
    public string Apellidos { get; set; }
    public string Correo { get; set; }
    public int Edad { get; set; }
    public string Contrasenia { get; set; }

    public Usuario(int id, string nombres, string apellidos, string correo, int edad, string contrasenia)
    {
        ID = id;
        Nombres = nombres;
        Apellidos = apellidos;
        Correo = correo;
        Edad = edad;
        Contrasenia = EncriptarContrasenia(contrasenia);
    }

    private string EncriptarContrasenia(string contrasenia)
    {
        // Implementación de SHA-256
    }

    public override string ToString()
    {
        return $"{ID}|{Nombres}|{Apellidos}|{Correo}|{Edad}|{Contrasenia}";
    }
}
```

### Vehículos

La clase Vehiculo representa los automóviles registrados en el taller:

```csharp
public class Vehiculo
{
    public int ID { get; set; }
    public int ID_Usuario { get; set; }
    public string Marca { get; set; }
    public int Modelo { get; set; }
    public string Placa { get; set; }

    public Vehiculo(int id, int idUsuario, string marca, int modelo, string placa)
    {
        ID = id;
        ID_Usuario = idUsuario;
        Marca = marca;
        Modelo = modelo;
        Placa = placa;
    }

    public override string ToString()
    {
        return $"{ID}|{ID_Usuario}|{Marca}|{Modelo}|{Placa}";
    }
}
```

### Repuestos

La clase Repuesto representa las piezas disponibles en el taller:

```csharp
public class Repuesto : IComparable<Repuesto>
{
    public int ID { get; set; }
    public string Nombre { get; set; }
    public string Detalles { get; set; }
    public double Costo { get; set; }

    public Repuesto(int id, string nombre, string detalles, double costo)
    {
        ID = id;
        Nombre = nombre;
        Detalles = detalles;
        Costo = costo;
    }

    public int CompareTo(Repuesto otro)
    {
        return ID.CompareTo(otro.ID);
    }

    public override string ToString()
    {
        return $"{ID}|{Nombre}|{Detalles}|{Costo}";
    }
}
```

### Servicios

La clase Servicio representa las tareas de mantenimiento realizadas:

```csharp
public class Servicio : IComparable<Servicio>
{
    public int ID { get; set; }
    public int ID_Repuesto { get; set; }
    public int ID_Vehiculo { get; set; }
    public string Detalles { get; set; }
    public double Costo { get; set; }

    public Servicio(int id, int idRepuesto, int idVehiculo, string detalles, double costo)
    {
        ID = id;
        ID_Repuesto = idRepuesto;
        ID_Vehiculo = idVehiculo;
        Detalles = detalles;
        Costo = costo;
    }

    public int CompareTo(Servicio otro)
    {
        return ID.CompareTo(otro.ID);
    }

    public override string ToString()
    {
        return $"{ID}|{ID_Repuesto}|{ID_Vehiculo}|{Detalles}|{Costo}";
    }
}
```

### Facturas

La clase Factura representa los comprobantes generados por los servicios:

```csharp
public class Factura
{
    public int ID { get; set; }
    public int ID_Servicio { get; set; }
    public double Total { get; set; }
    public string Fecha { get; set; }
    public string MetodoPago { get; set; }

    public Factura(int id, int idServicio, double total, string fecha, string metodoPago)
    {
        ID = id;
        ID_Servicio = idServicio;
        Total = total;
        Fecha = fecha;
        MetodoPago = metodoPago;
    }

    public override string ToString()
    {
        return $"{ID}|{ID_Servicio}|{Total}|{Fecha}|{MetodoPago}";
    }
}
```

## Algoritmos Principales

### Algoritmo de Blockchain

El algoritmo de Blockchain se implementa para garantizar la seguridad e integridad de los datos de usuario:

1. **Creación del Bloque Génesis**:
   - Se crea un bloque inicial con INDEX=0, PREVIOUS_HASH="0000".
   - Se genera el HASH utilizando SHA-256 sobre la concatenación de sus atributos.

2. **Adición de Nuevos Bloques**:
   - Se crea un nuevo bloque con el INDEX incrementado y PREVIOUS_HASH igual al HASH del último bloque.
   - Se realiza la prueba de trabajo (minado) incrementando el NONCE hasta obtener un HASH con el prefijo requerido.

3. **Verificación de la Cadena**:
   - Se recorre la cadena desde el bloque génesis.
   - Para cada bloque se verifica:
     - Que su HASH sea válido recalculándolo.
     - Que su PREVIOUS_HASH coincida con el HASH del bloque anterior.

```csharp
// Pseudocódigo para la verificación de la cadena
public bool ValidarCadena()
{
    for (int i = 1; i < cadena.Count; i++)
    {
        Bloque bloqueActual = cadena[i];
        Bloque bloqueAnterior = cadena[i - 1];

        // Verificar que el hash del bloque sea válido
        if (bloqueActual.Hash != bloqueActual.CalcularHash())
            return false;

        // Verificar que el bloque apunte correctamente al anterior
        if (bloqueActual.PreviousHash != bloqueAnterior.Hash)
            return false;
    }
    return true;
}
```

### Algoritmo de Huffman

El algoritmo de compresión Huffman se utiliza para reducir el tamaño de los reportes:

1. **Conteo de Frecuencias**:
   - Se cuenta la frecuencia de cada carácter en el texto.

2. **Construcción del Árbol**:
   - Se crea un nodo hoja para cada carácter.
   - Se insertan en una cola de prioridad según su frecuencia.
   - Se extraen los dos nodos con menor frecuencia y se combinan en un nuevo nodo padre.
   - Se repite hasta que quede un solo nodo (la raíz).

3. **Generación de Códigos**:
   - Se recorre el árbol desde la raíz hasta cada hoja.
   - Se asigna 0 para el camino izquierdo y 1 para el derecho.
   - Cada hoja recibe un código binario único.

4. **Compresión y Descompresión**:
   - Compresión: Se reemplaza cada carácter por su código correspondiente.
   - Descompresión: Se recorre el árbol según los bits del texto comprimido hasta encontrar una hoja.

```csharp
// Pseudocódigo para la generación de códigos
private void GenerarCodigos(NodoHuffman nodo, string codigo, Dictionary<char, string> tabla)
{
    if (nodo == null)
        return;

    if (nodo.EsHoja() && nodo.Caracter.HasValue)
        tabla.Add(nodo.Caracter.Value, codigo);

    GenerarCodigos(nodo.Izquierdo, codigo + "0", tabla);
    GenerarCodigos(nodo.Derecho, codigo + "1", tabla);
}
```

### Recorridos en Árboles

Se implementan los siguientes recorridos para los árboles utilizados en el sistema:

1. **In-Orden (Inorden)**:
   - Recorrer el subárbol izquierdo (recursivamente).
   - Visitar la raíz.
   - Recorrer el subárbol derecho (recursivamente).

2. **Pre-Orden (Preorden)**:
   - Visitar la raíz.
   - Recorrer el subárbol izquierdo (recursivamente).
   - Recorrer el subárbol derecho (recursivamente).

3. **Post-Orden (Postorden)**:
   - Recorrer el subárbol izquierdo (recursivamente).
   - Recorrer el subárbol derecho (recursivamente).
   - Visitar la raíz.

```csharp
// Recorrido In-Orden
public void InOrden(NodoBinario<T> nodo, List<T> resultado)
{
    if (nodo != null)
    {
        InOrden(nodo.Izquierdo, resultado);
        resultado.Add(nodo.Valor);
        InOrden(nodo.Derecho, resultado);
    }
}

// Recorrido Pre-Orden
public void PreOrden(NodoBinario<T> nodo, List<T> resultado)
{
    if (nodo != null)
    {
        resultado.Add(nodo.Valor);
        PreOrden(nodo.Izquierdo, resultado);
        PreOrden(nodo.Derecho, resultado);
    }
}

// Recorrido Post-Orden
public void PostOrden(NodoBinario<T> nodo, List<T> resultado)
{
    if (nodo != null)
    {
        PostOrden(nodo.Izquierdo, resultado);
        PostOrden(nodo.Derecho, resultado);
        resultado.Add(nodo.Valor);
    }
}
```

### Algoritmo de Árbol de Merkle

El algoritmo del Árbol de Merkle para la gestión de facturas:

1. **Construcción del Árbol**:
   - Se crea un nodo hoja para cada factura, calculando su hash.
   - Se agrupan los nodos de dos en dos y se crean nodos padres con el hash combinado.
   - Se repite el proceso hasta obtener un único nodo raíz.

2. **Verificación de Integridad**:
   - Se proporciona una transacción y una ruta de verificación (prueba).
   - Se recalcula el hash de la raíz utilizando la transacción y la prueba.
   - Se compara con el hash de la raíz almacenado.

```csharp
// Pseudocódigo para la construcción del árbol
private void ConstruirArbol()
{
    List<NodoMerkle> nodos = new List<NodoMerkle>();
    
    // Crear nodos hoja
    foreach (string transaccion in transacciones)
    {
        nodos.Add(new NodoMerkle(transaccion));
    }
    
    // Si hay un número impar de nodos, duplicar el último
    if (nodos.Count % 2 != 0)
        nodos.Add(new NodoMerkle(nodos[nodos.Count - 1].Data));
    
    // Construir niveles superiores del árbol
    while (nodos.Count > 1)
    {
        List<NodoMerkle> nuevoNivel = new List<NodoMerkle>();
        
        for (int i = 0; i < nodos.Count; i += 2)
        {
            NodoMerkle padre = new NodoMerkle(nodos[i], nodos[i + 1]);
            nuevoNivel.Add(padre);
        }
        
        nodos = nuevoNivel;
    }
    
    Raiz = nodos[0];
}
```

## Interfaz Gráfica

### Componentes GTK

La interfaz gráfica se desarrolla utilizando la biblioteca GTK# para C#. Los principales componentes utilizados son:

- **Window**: Ventana principal de la aplicación.
- **Box**: Contenedor para organizar widgets vertical u horizontalmente.
- **Button**: Botones para acciones del usuario.
- **Entry**: Campos de texto para entrada de datos.
- **Label**: Etiquetas para mostrar texto informativo.
- **TreeView**: Para mostrar datos en formato de tabla.
- **FileChooserDialog**: Para seleccionar archivos en el sistema.
- **Notebook**: Para crear interfaces con pestañas.

```csharp
// Ejemplo de creación de ventana principal
using Gtk;

public class MainWindow : Window
{
    private Button btnLogin;
    private Entry txtEmail;
    private Entry txtPassword;
    
    public MainWindow() : base("AutoGest Pro - Inicio de Sesión")
    {
        // Configurar ventana
        SetDefaultSize(400, 300);
        SetPosition(WindowPosition.Center);
        DeleteEvent += (o, args) => Application.Quit();
        
        // Crear componentes
        var vbox = new VBox(false, 5);
        vbox.BorderWidth = 10;
        
        var lblEmail = new Label("Correo:");
        txtEmail = new Entry();
        
        var lblPassword = new Label("Contraseña:");
        txtPassword = new Entry();
        txtPassword.Visibility = false;
        
        btnLogin = new Button("Iniciar Sesión");
        btnLogin.Clicked += OnLoginClicked;
        
        // Añadir componentes
        vbox.PackStart(lblEmail, false, false, 0);
        vbox.PackStart(txtEmail, false, false, 0);
        vbox.PackStart(lblPassword, false, false, 5);
        vbox.PackStart(txtPassword, false, false, 0);
        vbox.PackStart(btnLogin, false, false, 10);
        
        Add(vbox);
        ShowAll();
    }
    
    private void OnLoginClicked(object sender, EventArgs e)
    {
        // Implementación del inicio de sesión
    }
}
```

### Diseño de Ventanas

La aplicación incluye múltiples vent
