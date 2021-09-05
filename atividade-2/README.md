# Melhoria de códigos

## Método de validação de token

- Código antigo
```ts
const authValidate = (context: Context) => {
    const authHeader = context.req!.headers.authorization;
    
    if (authHeader) {
        const token = authHeader.split('Bearer ')[1];

        if (token) {
            try {
                const user = jwt.verify(token, SECRET_KEY);
                return user;
            } catch (err) {
                throw new AuthenticationError('Invalid/Expired token');
            }
        }
        throw new Error("Authentication token must be 'Bearer [token]'");
    }
    throw new Error('Authorization header must be provided.');
};
```
- Código melhorado
```ts
const authValidate = (context: Context) => {
    const authHeader = context.req!.headers.authorization;
    if (!authHeader) {
        throw new Error('Authorization header must be provided');
    }

    const token = authHeader.split('Bearer')[1].trim();

    if (!token) {
        throw new Error('Authentication must be \'Bearer [token]\'');
    }

    try {
        const user = jwt.verify(token, process.env.SECRET_KEY!);

        return user;
    } catch (err) {
        throw new AuthenticationError('Invalid or expired token');
    }
};
```

## Melhoria de atributos de um model

- Código antigo
```ts
@Entity('studant')
class Studant {
  @PrimaryColumn()
  readonly id: string;

  @ManyToOne(() => AccountRole, account_role => account_role.id)
  @JoinColumn({ name: 'account_role_id' })
  account_role: AccountRole;

  @ManyToOne(() => SchoolClass, school_class => school_class.id)
  @JoinColumn({ name: "school_class_id" })
  school_class: SchoolClass;

  @ManyToOne(() => Course, course => course.id)
  @JoinColumn({ name: "course_id" })
  course: Course;

  @Column()
  school_enrollment: string;

  @Column()
  name: string;

  @Column()
  sex: string;
  
  @Column()
  marital_status: string;

  @Column()
  birth_date: Date;

  @Column()
  education_level: string;

  @Column()
  father_name: string;

  @Column()
  mother_name: string;

  @Column()
  naturalness: string;

  @Column()
  nationality: string;

  @Column()
  phone_number: string;

  @Column()
  email: string;

  @Column({ select: false })
  password: string;

  @Column()
  rg: string;

  @Column()
  cpf: string;

  @Column()
  status: boolean;

  @CreateDateColumn()
  created_at: Date;

  @CreateDateColumn()
  updated_at: Date;
  
  @Column()
  street: string;

  @Column()
  number: number;

  @Column()
  district: string;

  @Column()
  complement: string;

  @Column()
  cep: string;

  @Column()
  city: string;

  @Column()
  state: string;

  constructor() {
    if (!this.id) {
      this.id = uuid();
    }

    if (!this.status) {
      this.status = true;
    }
  }
}
```

- Código melhorado
```ts

class BasicUser {
  @PrimaryColumn()
  readonly id: string;
  
  @CreateDateColumn()
  created_at: Date;

  @CreateDateColumn()
  updated_at: Date;
  
  constructor() {
    if (!this.id) {
      this.id = uuid();
    }

    if (!this.status) {
      this.status = true;
    }
  }
}

@Entity('user_address')
class UserAddress {
  @PrimaryColumn()
  id: string;

  @Column()
  user_id: string;

  @Column()
  street: string;

  @Column()
  number: number;

  @Column()
  district: string;

  @Column()
  complement: string;

  @Column()
  cep: string;

  @Column()
  city: string;

  @Column()
  state: string;

  @CreateDateColumn()
  created_at: Date;

  @CreateDateColumn()
  updated_at: Date;

  constructor() {
    if (!this.id) {
      this.id = uuid();
    }
  }
}

@Entity('studant')
class Studant extends BasicUser {
  @ManyToOne(() => AccountRole, account_role => account_role.id)
  @JoinColumn({ name: 'account_role_id' })
  account_role: AccountRole;

  @ManyToOne(() => SchoolClass, school_class => school_class.id)
  @JoinColumn({ name: "school_class_id" })
  school_class: SchoolClass;

  @ManyToOne(() => Course, course => course.id)
  @JoinColumn({ name: "course_id" })
  course: Course;
  
  @OneToOne(() => UserAddress)
  @JoinColumn()
  address: UserAddress;

  @Column()
  school_enrollment: string;

  @Column()
  name: string;

  @Column()
  sex: string;
  
  @Column()
  marital_status: string;

  @Column()
  birth_date: Date;

  @Column()
  education_level: string;

  @Column()
  father_name: string;

  @Column()
  mother_name: string;

  @Column()
  naturalness: string;

  @Column()
  nationality: string;

  @Column()
  phone_number: string;

  @Column()
  email: string;

  @Column({ select: false })
  password: string;

  @Column()
  rg: string;

  @Column()
  cpf: string;

  @Column()
  status: boolean;
  
}
```
