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

    public boolean isSuitableForPromotion() {
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

    // atributos, getters e setters...

}

class HumanRecoursesService {
   public boolean isSuitableForPromotion(Employee employee) {
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
ibterface EmployeeRole {
    double getBasePayAmount();
}

public class Recruiter extends Employee implements EmployeeRole {
    public double getBasePayAmount() {
        return 2000;
    }
}

public class Manager extends Employee implements EmployeeRole {
    public double getBasePayAmount() {
        return 3500;
    }
}

private class Programmer extends Employee implements EmployeeRole {
    public double getBasePayAmount() {
        return 6000;
    }
}
```

## L - Liskov Substitution Principle

Antes:

```java
public class Employee {
    // atributos, getters e setters
    
    public void sendJobProposalEmail() {
        // Enviar e-mail para possível candidato
    }
}

public class Recruiter extends Employee implements EmployeeRole {}

private class Programmer extends Employee implements EmployeeRole {}

// Recruiter recruiter = new Recruiter();
// recruiter.sendJobProposalEmail(); 😀

// Programmer programmer = new Programmer();
// programmer.sendJobProposalEmail(); 🤔
```

Depois:

```java
public class Employee {}

public class HRSectorEmployee extends Employee {
    public void sendJobProposalEmail() {
        // Enviar e-mail para possível candidato
    }
}

public class ITSectorEmployee extends Employee {}

public class Recruiter extends HRSectorEmployee Employee implements EmployeeRole {}

private class Programmer extends ITSectorEmployee implements EmployeeRole {}
```

## I - Interface Segregation Principle

Antes:

```java
public interface InterviewSchedule {
    public void schedulePresentialInterview();
    public void scheduleOnlineInterview();
}

public class PresentialInterviewScheduleImpl implements InterviewSchedule {
    public void schedulePresentialInterview() {
        // implementação do método
    }
    
    public void scheduleOnlineInterview() {
        throw new UnsupportedOperationException();
    }
}

public class OnlineInterviewScheduleImpl implements InterviewSchedule {
    public void schedulePresentialInterview() {
        throw new UnsupportedOperationException();
    }
    
    public void scheduleOnlineInterview() {
        // implementação do método
    }
}
```

Depois:

```java
public interface PresentialInterviewSchedule {
    public void schedulePresentialInterview();
}

public interface OnlineInterviewSchedule {
    public void scheduleOnlineInterview();
}

public class PresentialInterviewScheduleImpl implements PresentialInterviewSchedule {
    public void schedulePresentialInterview() {
        // implementação do método
    }
}

public class OnlineInterviewScheduleImpl implements OnlineInterviewSchedule {
    public void scheduleOnlineInterview() {
        // implementação do método
    }
}
```

## D - Dependency Inversion Principle

Antes:

```java
public class EmployeeNotificationService {

   private Recruiter recruiter;
   
   private Programmer programmer;
   
   public sendNotificationToRecruiter(Recruiter recruiter) {
        // enviar notificação para recrutador;
   }
   
   public sendNotificationToProgrammer(Programmer programmer) {
        // enviar notificação para programador;
   }

}
```

Depois:

```java
public class EmployeeNotificationService {

   private EmployeeRole employee;
   
   public sendNotificationToEmployee(Employee employee) {
        // enviar notificação para empregado;
   }

}
```
