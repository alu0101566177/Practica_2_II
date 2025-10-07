# Practica_2_II

## Ejercicio 1

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

```csharp
```

## Ejercicio 8

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