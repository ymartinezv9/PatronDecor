# PatronDecor
Explicacion y ejemplo de uso del patron deseño Decor

## 1. ¿Qué es el patrón Decorator?
El patrón **Decorator** es un patrón de diseño estructural que permite añadir comportamientos adicionales a un objeto de forma dinámica sin alterar su estructura original. 
En lugar de utilizar herencia para extender las funcionalidades, el patrón Decorator se basa en la composición, envolviendo objetos con decoradores que añaden nuevas características.

Este patrón es útil cuando se necesita extender la funcionalidad de un objeto de manera flexible y modular, sin modificar su código base. 
Cada decorador es una clase que "envuelve o decora" al objeto original y puede añadirle comportamientos nuevos o modificar los ya existentes.

## 2. Ventajas del patrón Decorator
- **Extensibilidad**: Permite agregar nuevas funcionalidades sin modificar el código base.
- **Combinación dinámica**: Los objetos pueden ser decorados con múltiples decoradores para agregar combinaciones de comportamientos.
- **Simplicidad en la modificación**: No es necesario modificar todas las clases si quieres añadir una funcionalidad nueva.

## 3. Ejemplo del Patrón Decorator: Estudiantes de la UMG

En este ejemplo, tenemos estudiantes en la **UMG** y queremos decorarlos con características adicionales como "Estudiante con Beca" o "Estudiante Miembro de Club". 
Utilizamos el patrón **Decorator** para agregar estas características de manera flexible.

### Código en Java

```java
// Componente base
interface Estudiante {
    String getDescripcion();
    double getCostoMatricula();
}

// Componente concreto
class EstudianteUMG implements Estudiante {
    @Override
    public String getDescripcion() {
        return "Estudiante de la UMG";
    }

    @Override
    public double getCostoMatricula() {
        return 1500.0;  // Costo de la matrícula base
    }
}

// Decorador abstracto
abstract class EstudianteDecorador implements Estudiante {
    protected Estudiante estudianteDecorado;

    public EstudianteDecorador(Estudiante estudiante) {
        this.estudianteDecorado = estudiante;
    }

    @Override
    public String getDescripcion() {
        return estudianteDecorado.getDescripcion();
    }

    @Override
    public double getCostoMatricula() {
        return estudianteDecorado.getCostoMatricula();
    }
}

// Decorador concreto: añade beca
class EstudianteConBeca extends EstudianteDecorador {
    public EstudianteConBeca(Estudiante estudiante) {
        super(estudiante);
    }

    @Override
    public String getDescripcion() {
        return estudianteDecorado.getDescripcion() + ", con Beca";
    }

    @Override
    public double getCostoMatricula() {
        return estudianteDecorado.getCostoMatricula() - 700;  // Descuento por la beca
    }
}

// Decorador concreto: añade membresía a un club
class EstudianteConClub extends EstudianteDecorador {
    public EstudianteConClub(Estudiante estudiante) {
        super(estudiante);
    }

    @Override
    public String getDescripcion() {
        return estudianteDecorado.getDescripcion() + ", miembro del Club de Tecnología";
    }

    @Override
    public double getCostoMatricula() {
        return estudianteDecorado.getCostoMatricula() + 300;  // Costo adicional por el club
    }
}

// Uso del patrón Decorator
public class Main {
    public static void main(String[] args) {
        // Estudiante regular
        Estudiante estudiante = new EstudianteUMG();
        System.out.println(estudiante.getDescripcion() + " - Costo: $" + estudiante.getCostoMatricula());

        // Estudiante con beca
        Estudiante estudianteBecado = new EstudianteConBeca(estudiante);
        System.out.println(estudianteBecado.getDescripcion() + " - Costo: $" + estudianteBecado.getCostoMatricula());

        // Estudiante con beca y miembro de un club
        Estudiante estudianteBecaYClub = new EstudianteConClub(estudianteBecado);
        System.out.println(estudianteBecaYClub.getDescripcion() + " - Costo: $" + estudianteBecaYClub.getCostoMatricula());
    }
}
```
### Explicación:
- **Estudiante**: Es la interfaz base que define las características de los estudiantes.
- **EstudianteUMG**: Es el componente concreto, que representa a un estudiante regular de la UMG.
- **EstudianteDecorador**: Es una clase abstracta que implementa la interfaz `Estudiante` y sirve como base para los decoradores.
- **EstudianteConBeca**: Es un decorador concreto que añade la funcionalidad de "Estudiante con Beca", aplicando un descuento en la matrícula.
- **EstudianteConClub**: Es otro decorador concreto que añade la funcionalidad de "Miembro del Club de Tecnología", lo que añade un costo extra.

### Resultado en consola:
```bash
Estudiante de la UMG - Costo: $1500.0
Estudiante de la UMG, con Beca - Costo: $800.0
Estudiante de la UMG, con Beca, miembro del Club de Tecnología - Costo: $1100.0
```
### Conclusión
El patrón **Decorator** es una solución eficaz para agregar comportamientos adicionales a un objeto de forma dinámica y flexible, sin modificar su estructura interna. En este ejemplo, los estudiantes de la UMG pueden tener características adicionales como ser becados o miembros de un club, y estas características pueden combinarse según sea necesario.


