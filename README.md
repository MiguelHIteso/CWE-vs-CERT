## Common Weakness Enumeration (CWE) Framework

El **CWE Framework** es un sistema de enumeración y descripción de debilidades de seguridad comunes en software y hardware. CWE proporciona un lenguaje común y una taxonomía para identificar, entender y mitigar estas debilidades. Cada debilidad se identifica mediante un número y se describe en detalle en una entrada CWE.

## CERT Secure Coding Standards

Los **CERT Secure Coding Standards** son un conjunto de pautas y reglas para escribir código seguro y libre de vulnerabilidades. Estas normas son desarrolladas por el **CERT Coordination Center** y se centran en mitigar las debilidades de seguridad comunes identificadas en el marco CWE. Los estándares del CERT están diseñados para ayudar a los desarrolladores a escribir código seguro desde el principio.

### Similitudes entre CWE y CERT Secure Coding Standards

1. **Enfoque en debilidades de seguridad:** Tanto CWE como los estándares del CERT se centran en identificar y mitigar debilidades de seguridad comunes en el software.

2. **Clasificacion de vulnerabilidades:** Ambos utilizan metricas para clasificar los niveles de las vulnerabilidades.

3. **Taxonomía:** CWE proporciona una taxonomía de debilidades, mientras que los estándares del CERT ofrecen reglas y pautas específicas para evitar estas debilidades en el código.

#### Evitar Inyección SQL

```java
public class SQLInjectionExample {

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.print("Ingrese su nombre de usuario: ");
        String userInput = scanner.nextLine();

        // Establecer la conexión a la base de datos (reemplaza con tu información de conexión)
        String jdbcUrl = "jdbc:mysql://localhost:3306/mydb";
        String dbUser = "user";
        String dbPassword = "password";

        try (Connection connection = DriverManager.getConnection(jdbcUrl, dbUser, dbPassword);
             Statement statement = connection.createStatement()) {

            // Ejemplo de inyección SQL intencionada
            String sql = "SELECT * FROM users WHERE username='" + userInput + "'"; // CWE-89: SQL Injection
            ResultSet resultSet = statement.executeQuery(sql);

            while (resultSet.next()) {
                String username = resultSet.getString("username");
                System.out.println("Usuario encontrado: " + username);
            }

        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```

#### Evitar desbordamiento del Buffer

```c
#include <stdio.h>
#include <string.h>

void processInput(char *input) {
    char buffer[10];
    strcpy(buffer, input); // CWE-120: Buffer Overflow
    // ...
}

int main() {
    char userInput[20];
    printf("Ingrese su nombre: ");
    gets(userInput); // CWE-242: Use of Insecure Function
    processInput(userInput);
    return 0;
}
```
#### Validacion de entrada

```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.print("Ingrese su edad: ");
        int age = scanner.nextInt();
        if (age < 0) { // CWE-129: Improper Validation of Array Index
            System.out.println("Edad no válida.");
        } else {
            System.out.println("Edad válida: " + age);
        }
    }
}```

