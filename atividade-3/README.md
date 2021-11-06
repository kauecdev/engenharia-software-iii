# Aplicação dos conceitos SOLID na prática

## Sistema de Gerenciamento de Recursos Humanos

## S - Single Responsability Principle

Antes:

```java
public class Employee {

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
public class Employee {

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

Antes:

```java
public double getBasePayAmountByRole(Role role) {
    switch(role) {
        case RoleEnum.RECRUITER:
            return 2000;
        case RoleEnum.MANAGER:
            return 3500;
        // outras possíveis roles no sistema
    }
}
```

Depois:

```java
abstract class EmployeeRole {
    abstract double getBasePayAmount();
}

public class Recruiter extends EmployeeRole {
    private double getBasePayAmount() {
        return 2000;
    }
}

public class MANAGER extends EmployeeRole {
    private double getBasePayAmount() {
        return 3500;
    }
}
```

## L - Liskov Substitution Principle 

## I - Interface Segregation Principle

## D - Dependency Inversion Principle
