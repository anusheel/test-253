---
system_prompt: For any parts of your response that include code, make sure to include the filename along with the backtick and the code snippets. For any environment variables, use stubuser and stubpassword as the login. For any commands, auto confirm any prompts on stdin. 
model: gpt-4-0613
temperature: 0
---



### Create your prompts below and Stub will generate the code and documentation


```stub
Create a high quality codebase with NestJS and TypeORM for all the CRUD API endpoints with the following 2 entities:
- User, with attributes : name, email
- Todo, with attributes : title, description, assignee
Assignee attribute in Todo is of type User, with each todo having a unique optional user as the assignee.

Use nest generate resource command
```

<details open id="f1e0308aac77c15b6b2047d2dc87a840">
<summary></summary>

Firstly, you need to install NestJS CLI globally on your machine. You can do this by running the following command:

```bash
npm i -g @nestjs/cli
```

Then, create a new project:

```bash
nest new nestjs-typeorm-crud
```

Navigate into the project directory:

```bash
cd nestjs-typeorm-crud
```

Install the necessary packages:

```bash
npm install @nestjs/typeorm typeorm pg
```

Now, let's generate the resources for User and Todo:

```bash
nest generate resource user
```

When prompted, select `REST API`, `Y` for generating CRUD entry points, and `N` for generating spec files.

Do the same for Todo:

```bash
nest generate resource todo
```

This will generate all the necessary files for User and Todo resources.

Next, you need to configure TypeORM. Create a file named `ormconfig.json` in the root directory of your project and add the following configuration:

```json
{
  "type": "postgres",
  "host": "localhost",
  "port": 5432,
  "username": "stubuser",
  "password": "stubpassword",
  "database": "test",
  "entities": ["dist/**/*.entity{.ts,.js}"],
  "synchronize": true
}
```

Now, let's define our entities. In `user.entity.ts`:

```typescript
import { Entity, Column, PrimaryGeneratedColumn, OneToMany } from 'typeorm';
import { Todo } from '../todo/todo.entity';

@Entity()
export class User {
  @PrimaryGeneratedColumn()
  id: number;

  @Column()
  name: string;

  @Column()
  email: string;

  @OneToMany(() => Todo, (todo) => todo.assignee)
  todos: Todo[];
}
```

And in `todo.entity.ts`:

```typescript
import { Entity, Column, PrimaryGeneratedColumn, ManyToOne } from 'typeorm';
import { User } from '../user/user.entity';

@Entity()
export class Todo {
  @PrimaryGeneratedColumn()
  id: number;

  @Column()
  title: string;

  @Column()
  description: string;

  @ManyToOne(() => User, (user) => user.todos)
  assignee: User;
}
```

This sets up a basic NestJS application with TypeORM for CRUD operations on User and Todo entities. You can now run your application with `npm run start:dev`.
</details>

