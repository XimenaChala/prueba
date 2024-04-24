# Estudiantes
crear un sistema para gestionar la información de estudiantes y sus calificaciones. cada estudiante tiene un nombre y un numero de identidad único.   mientras que cada calificación este asociado a  un estudiante y tiene una materia y una nota  Control y seguimiento 

## Análisis: Definición de Requerimientos

#### Registro de Estudiantes: 
* Cada estudiante debe tener un nombre único y un número de identidad único para su registro en el sistema.

#### Gestión de Calificaciones:
* Cada calificación debe estar asociada a un estudiante.
* Se debe registrar la materia a la que corresponde la calificación.
* Registrar la nota obtenida por el estudiante en esa materia.
#### Interfaz de Usuario:
* Debe permitir la fácil inserción, modificación y eliminación de estudiantes y sus calificaciones.
* Debe ser intuitiva y fácil de usar para cualquier usuario.
#### Seguridad y Privacidad:
* Acceso restringido solo a usuarios autorizados.
* Los datos de los estudiantes y sus calificaciones deben mantenerse confidenciales y seguros.

#### Funcionalidades Adicionales:
* Búsqueda rápida de estudiantes por nombre o número de identidad.
* Generación de reportes de calificaciones por estudiante, materia o período.
* Posibilidad de agregar comentarios o notas adicionales a las calificaciones.

#### Escalabilidad:
* El sistema debe ser capaz de manejar un gran número de estudiantes y sus calificaciones sin comprometer el rendimiento.

#### Personalización:
* Permitir la configuración de parámetros como el formato de las calificaciones, el período académico, etc.
#### Respaldo y Recuperación:
* Implementar un sistema de respaldo regular para evitar la pérdida de datos.
* Capacidad para recuperar datos en caso de fallo del sistema o error humano.
#### Integración:
* Posibilidad de integrar el sistema con otros sistemas de gestión escolar o herramientas educativas existentes.
#### Documentación y Soporte:
* Proporcionar documentación detallada sobre el uso del sistema.
* Ofrecer soporte técnico para resolver cualquier problema o duda que puedan tener los usuarios.

#### Diseñar Base de Datos
Datos a tener en cuenta

| Número de Identidad | Nombre del Estudiante | Materia |  Nota |
|---------------------|-----------------------|---------|-------|
|  123432             |   pablo guzman        | español |  3.5  |
|  1354556            |   andrea lopez        | ingles  |  2.0  |
|  23557773           |   carlos zapata       | etica   |  4.0  |
|  2345665            |   pedro castro        | fisica  |  3.9  |

* En esta tabla, cada fila representa a un estudiante y sus atributos están normalizados en dos columnas separadas: "Número de Identidad" y "Nombre del Estudiante". Esto permite una gestión más eficiente de los datos, evitando la redundancia al tener múltiples entradas del mismo nombre de estudiante, y facilitando la integridad y consistencia de la información.

 En este sentido, se procede a normarlizar de la siguiente manera.

* Esta normalización nos brinda flexibilidad para realizar consultas y operaciones específicas sobre los estudiantes sin necesidad de repetir la información básica en cada registro de calificación. 

`Estudiantes`
| GruposID | numero de identidad | Asignatura| Notas |
|----------|---------------------|-----------|-------|
|  101     | 123432              | español   | 3.5   |
|  201     | 1354556             | ingles    | 2.0   |
|  304     | 23557773            | etica     | 4.0   |
|  405     | 2345665             | fisica    | 3.9   |

* Se conoce que al finalizar cada profesor ,debe profesor debe organizar los `grupos` para calificar las notas de cada estudiante, dependiendo de la asignatura y horario.

`Asignatura`
| GruposID | Asignatura | Profesor  |horarios |
|----------|------------|-----------|---------|
|  101     | español    | Peña      | mañana  |
|  201     | ingles     | Manrique  | tarde   |
|  304     | etica      | Lopez     | mañana  |
|  405     | fisica     | Cruz      | tarde   |

>ver
![Modelo relacional del ejercicio](image.png) 

> Script de la base de datos
```sql
   DROP DATABASE IF EXISTS Asignatura;
   
    create database Asignatura;
    
    use Asignatura;

    CREATE table Estudiantes(

     GrupoID int not null primary key auto_increment,
     Numero_Identidad int not null unique,
     Asignatura nvarchar(50) not null,
     Notas int not null,
     FOREIGN KEY (Asignatura) REFERENCES Asignatura(Profesor)
    );
    CREATE table Asignatura(
        GrupoID INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
        Asignatura_Profesor VARCHAR(50) NOT NULL,
        Profesor DATE NOT NULL,
        Horario INT NOT NULL,
        FOREIGN KEY (Grupo_ID) REFERENCES Grupo(ID)
    ); 
```

