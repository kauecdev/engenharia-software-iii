# Aplicação dos conceitos SOLID na prática

## Sistema de Gerenciamento de Recursos Humanos

## S - Single Responsability Principle

Antes:

```java
class Employee {

    private String id;

    private String name;

    private RoleEnum role;

    private Date joiningDate;

    // atributos, getters and setters...

    private boolean isSuitableForPromotion() {
        // algoritmo para calcular tempo trabalhado, serviços prestados
        // e outros fatores que determinem sua promoção
    }

}
```

Depois:

```java
class Employee {

    private String id;

    private String name;

    private RoleEnum role;

    private Date joiningDate;

    // atributos, getters and setters...

}

class HumanRecoursesService {
   private boolean isSuitableForPromotion(Employee employee) {
        // algoritmo para calcular tempo trabalhado, serviços prestados
        // e outros fatores que determinem sua promoção
   }
}
```

## O - Open/Closed Principle

## L - Liskov Substitution Principle 

## I - Interface Segregation Principle

## D - Dependency Inversion Principle
