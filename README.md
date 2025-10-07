# Practica_2_II

## Ejercicio 1

Cada 120 fotogramas, el objeto cambia su color a uno aleatorio y se mueve a una nueva posición aleatoria dentro de un rango de 10 unidades en los ejes X, Y y Z.

```csharp
using UnityEngine;

public class Ej_1_Color : MonoBehaviour
{
    private int frame = 0;

    private Color GenerateColor()
    {
        return new Color(Random.value, Random.value, Random.value);
    }

    private Vector3 GeneratePos()
    {
        int displacement = 10;
        return new Vector3(Random.value * displacement, Random.value * displacement, Random.value * displacement);
    }

    void Start()
    {
        
    }

    void Update()
    {
        ++frame;
        if (frame % 120 != 0) return;

        GetComponent<Renderer>().material.color = this.GenerateColor();
        this.gameObject.transform.position = this.GeneratePos();
    }
}
```

## Ejercicio 2

Calcula y muestra en la consola la magnitud de dos vectores, el ángulo entre ellos, la distancia que los separa y cuál de los dos está más alto según su componente Y.

```csharp
using UnityEngine;

public class Ej_2_Pos : MonoBehaviour
{
    public Vector3 vectorA;
    public Vector3 vectorB;

    void Start()
    {
        float magnitudA = vectorA.magnitude;
        float magnitudB = vectorB.magnitude;
        float angulo = Vector3.Angle(vectorA, vectorB);
        float distancia = Vector3.Distance(vectorA, vectorB);

        string mayorAltura;
        if (vectorA.y > vectorB.y)
            mayorAltura = "Vector A está más alto";
        else if (vectorB.y > vectorA.y)
            mayorAltura = "Vector B está más alto";
        else
            mayorAltura = "Ambos tienen la misma altura";

        Debug.Log($"Magnitud de A: {magnitudA}");
        Debug.Log($"Magnitud de B: {magnitudB}");
        Debug.Log($"Ángulo entre A y B: {angulo} grados");
        Debug.Log($"Distancia entre A y B: {distancia}");
        Debug.Log(mayorAltura);
    }
}
```

## Ejercicio 3

Al iniciar la escena, muestra en la consola la posición actual del objeto (por ejemplo, una esfera).

```csharp
public class Ej_3 : MonoBehaviour
{
    void Start()
    {
        Debug.Log($"Posición actual de la esfera: {GetComponent<Transform>().position}");
    }
}
```

## Ejercicio 4

Encuentra los objetos con las etiquetas `"Cube"` y `"Cylinder"`, y calcula la distancia entre el objeto actual (por ejemplo, una esfera) y cada uno de ellos, mostrando los resultados en consola.

```csharp
using UnityEngine;

public class Ej_4 : MonoBehaviour
{
    private GameObject cube;
    private GameObject cylinder;

    void Start()
    {
        cube = GameObject.FindWithTag("Cube");
        cylinder = GameObject.FindWithTag("Cylinder");

        float distCube = Vector3.Distance(transform.position, cube.transform.position);
        Debug.Log($"Distancia entre la esfera y el cubo: {distCube}");

        float distCylinder = Vector3.Distance(transform.position, cylinder.transform.position);
        Debug.Log($"Distancia entre la esfera y el cilindro: {distCylinder}");
    }
}
```

## Ejercicio 5

Cada vez que se presiona la barra espaciadora, el objeto se mueve a la posición de uno de los tres objetos asignados. Va alternando entre ellos en orden secuencial.

```csharp
using UnityEngine;

public class Ej_5 : MonoBehaviour
{
    public Transform objeto1;
    public Transform objeto2;
    public Transform objeto3;

    private int counter = 0;

    void Start()
    {
    }

    void Update()
    {
        if (Input.GetKeyDown(KeyCode.Space))
        {
            Debug.Log("Barra espaciadora pulsada → moviendo objetos...");

            if (counter % 3 == 0)
                this.gameObject.transform.position = objeto1.position;

            if (counter % 3 == 1)
                this.gameObject.transform.position = objeto2.position;

            if (counter % 3 == 2)
                this.gameObject.transform.position = objeto3.position;

            counter++;
        }
    }
}
```

## Ejercicio 6

Cuando se presionan las teclas de flecha, se muestra en consola el valor de movimiento calculado en función de la velocidad y la dirección presionada (sin mover realmente el objeto).


```csharp
using UnityEngine;

public class Ej_6 : MonoBehaviour
{
    public float velocity = 2f;

    void Update()
    {
        float horizontal = Input.GetAxis("Horizontal");
        float vertical = Input.GetAxis("Vertical");

        if (Input.GetKeyDown(KeyCode.RightArrow))
        {
            Debug.Log($"Flecha Derecha: {velocity * horizontal}");
        }

        if (Input.GetKeyDown(KeyCode.LeftArrow))
        {
            Debug.Log($"Flecha Izquierda: {velocity * horizontal}");
        }

        if (Input.GetKeyDown(KeyCode.UpArrow))
        {
            Debug.Log($"Flecha Arriba: {velocity * vertical}");
        }

        if (Input.GetKeyDown(KeyCode.DownArrow))
        {
            Debug.Log($"Flecha Abajo: {velocity * vertical}");
        }
    }
}
```

## Ejercicio 7

1. En Unity, **Edit → Project Settings → Input Manager**.
2. Expande la lista de **Axes**.
3. Duplica una entrada existente (por ejemplo, “Fire1”) y cámbiale el nombre a **“Disparo”**.
4. En la propiedad **Positive Button**, escribe la tecla **`h`** (minúscula).
5. Guarda los cambios.

Ahora la tecla **H** activará la acción de disparo definida en el código.

## Ejercicio 8

El objeto se mueve constantemente en una dirección determinada. Si `localSpace` es `true`, se mueve según su propia orientación; si es `false`, se mueve en el espacio global.

```csharp
using UnityEngine;

public class Ej_8 : MonoBehaviour
{
    public Vector3 moveDirection = new Vector3(1f, 0f, 0f);
    public float speed = 2f;
    public bool localSpace = false;

    void Start()
    {
        Vector3 startPos = transform.position;
        startPos.y = 0f;
        transform.position = startPos;
    }

    void Update()
    {
        Vector3 desplazamiento = moveDirection.normalized * speed;

        if (localSpace)
        {
            transform.Translate(desplazamiento, Space.Self);
        }
        else
        {
            transform.Translate(desplazamiento, Space.World);
        }
    }
}
```

## Ejercicio 9

Permite mover el objeto usando las teclas **WASD** si `sphere` es `true`, o las **flechas** si es `false`. El movimiento no depende del tiempo, por lo que la velocidad puede variar según el framerate.

```csharp
using UnityEngine;

public class Ej_9 : MonoBehaviour
{
    public float speed = 5f;
    public bool sphere = false;

    void Update()
    {
        Vector3 move = Vector3.zero;

        if (sphere)
        {
            if (Input.GetKey(KeyCode.W)) move.z += 1f;
            if (Input.GetKey(KeyCode.S)) move.z -= 1f;
            if (Input.GetKey(KeyCode.A)) move.x -= 1f;
            if (Input.GetKey(KeyCode.D)) move.x += 1f;
        }
        else
        {
            if (Input.GetKey(KeyCode.UpArrow)) move.z += 1f;
            if (Input.GetKey(KeyCode.DownArrow)) move.z -= 1f;
            if (Input.GetKey(KeyCode.LeftArrow)) move.x -= 1f;
            if (Input.GetKey(KeyCode.RightArrow)) move.x += 1f;
        }

        transform.Translate(move.normalized * speed, Space.World);
    }
}
```

## Ejercicio 10

Similar al Ejercicio 9, pero el movimiento ahora está multiplicado por `Time.deltaTime`, haciendo que la velocidad sea constante independientemente del framerate.

```csharp
using UnityEngine;

public class Ej_10 : MonoBehaviour
{
    public float speed = 5f;
    public bool sphere = false;

    void Update()
    {
        Vector3 move = Vector3.zero;

        if (sphere)
        {
            if (Input.GetKey(KeyCode.W)) move.z += 1f;
            if (Input.GetKey(KeyCode.S)) move.z -= 1f;
            if (Input.GetKey(KeyCode.A)) move.x -= 1f;
            if (Input.GetKey(KeyCode.D)) move.x += 1f;
        }
        else
        {
            if (Input.GetKey(KeyCode.UpArrow)) move.z += 1f;
            if (Input.GetKey(KeyCode.DownArrow)) move.z -= 1f;
            if (Input.GetKey(KeyCode.LeftArrow)) move.x -= 1f;
            if (Input.GetKey(KeyCode.RightArrow)) move.x += 1f;
        }

        transform.Translate(move.normalized * speed * Time.deltaTime, Space.World);
    }
}
```

## Ejercicio 11

El objeto se mueve automáticamente hacia la posición de una esfera (`esferaTransform`) ignorando la diferencia en el eje Y. Simula un “seguimiento” constante.

```csharp
using UnityEngine;

public class Ej_11 : MonoBehaviour
{
    public float speed = 5f;
    public Transform esferaTransform;

    void Start()
    {
        
    }

    void Update()
    {
        Vector3 direction = esferaTransform.position - transform.position;
        direction.y = 0f;
        transform.Translate(direction.normalized * speed * Time.deltaTime, Space.World);
    }
}
```

## Ejercicio 12

El objeto siempre **mira hacia la esfera** y avanza hacia ella a una velocidad constante, rotando suavemente para orientarse en su dirección.

```csharp
using UnityEngine;

public class Ej_12 : MonoBehaviour
{
    public float speed = 3f;
    public Transform sphere;

    void Update()
    {

        Vector3 targetPos = sphere.position;
        targetPos.y = transform.position.y;
        transform.LookAt(targetPos);
        transform.Translate(Vector3.forward * speed * Time.deltaTime, Space.Self);
    }
}
```

## Ejercicio 13

El objeto avanza continuamente hacia adelante y gira según el eje horizontal (izquierda/derecha). Además, dibuja una línea roja (raycast visual) para indicar su dirección actual.

```csharp
using UnityEngine;

public class Ej_13 : MonoBehaviour
{
    public float speed = 5f;
    public float rotationSpeed = 100f;

    void Update()
    {
        float h = Input.GetAxis("Horizontal");
        transform.Rotate(0f, h * rotationSpeed * Time.deltaTime, 0f);
        transform.Translate(transform.forward * speed * Time.deltaTime, Space.World);
        Debug.DrawRay(transform.position, transform.forward * 2f, Color.red);
    }
}
```