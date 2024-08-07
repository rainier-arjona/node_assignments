### tsconfig.json
```json
{
  "compilerOptions": {
    "target": "ES6",
    "module": "commonjs",
    "strict": true,
    "esModuleInterop": true,
    "skipLibCheck": true,
    "outDir": "./dist",
    "rootDir": "./src",
    "resolveJsonModule": true
  },
  "include": [
    "src/**/*"
, "src/config"  ],
  "exclude": [
    "node_modules",
    "dist"
  ]
}
```

### package.json
```json
{
  "name": "02-employees-i",
  "version": "1.0.0",
  "main": "index.js",
  "scripts": {
    "build": "tsc",
    "sync": "node dist/sync.js",
    "migrate": "sequelize db:migrate --config src/config/config.json",
    "migrate:undo": "sequelize db:migrate:undo --config src/config/config.json",
    "seed": "sequelize db:seed:all --config src/config/config.json",
    "seed:undo": "sequelize db:seed:undo --config src/config/config.json",
    "start": "node dist/server.js",
    "dev": "tsc-watch --onSuccess \"nodemon dist/server.js\"",
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "description": "",
  "dependencies": {
    "dotenv": "^16.4.5",
    "mysql2": "^3.11.0",
    "sequelize": "^6.37.3",
    "tsc-watch": "^6.2.0"
  },
  "devDependencies": {
    "@types/express": "^4.17.21",
    "@types/node": "^22.0.0",
    "nodemon": "^3.1.4",
    "sequelize-cli": "^6.6.2",
    "ts-node": "^10.9.2",
    "ts-node-dev": "^2.0.0",
    "typescript": "^5.5.4"
  }
}
```

### src/config/config.json
```json
{
    "development": {
        "username": "root",
        "password": "root",
        "database": "management_db",
        "host": "127.0.0.1",
        "dialect": "mysql"
    },
}
```
### src/config/database.ts
```ts
import { Sequelize } from 'sequelize';
import dotenv from 'dotenv';

dotenv.config();

const sequelize = new Sequelize(
    process.env.DB_NAME!,
    process.env.DB_USERNAME!,
    process.env.DB_PASSWORD!,
    {
        host: process.env.DB_HOST,
        dialect: process.env.DB_DIALECT as 'mysql',
    }
);

export default sequelize;
```

### .env
```js
DB_USERNAME=root
DB_PASSWORD=root
DB_NAME=management_db
DB_HOST=127.0.0.1
DB_DIALECT=mysql
```

### src/sync.ts
```ts
import sequelize from './config/database';
import "./models";

const syncDatabase = async () => {
    try {
        // Check database connection
        await sequelize.authenticate();
        console.log('Connection has been established successfully.');

        // Synchronize the models with the database
        await sequelize.sync({ force: true }); // Creates tables or drops them if they exist
        console.log('Database synchronized');
    } catch (error) {
        console.error('Error:', error);
    }
};

syncDatabase();
```
### src/models/index.ts
```ts
import { Employee } from './employee';
import { Project } from './project';
import { Task } from './task';

export { Employee, Project, Task };
```

### src/models/employee.ts
```ts
import { Model, DataTypes } from 'sequelize';
import sequelize from '../config/database';

class Employee extends Model {
    public id!: number;
    public firstName!: string;
    public lastName!: string;
    public email!: string;
    public hireDate!: Date;
    public salary!: number;
}

Employee.init({
    id: {
        type: DataTypes.INTEGER,
        autoIncrement: true,
        primaryKey: true,
    },
    firstName: {
        type: DataTypes.STRING,
        allowNull: false,
    },
    lastName: {
        type: DataTypes.STRING,
        allowNull: false,
    },
    email: {
        type: DataTypes.STRING,
        unique: true,
        allowNull: false,
    },
    hireDate: {
        type: DataTypes.DATE,
        allowNull: false,
    },
    salary: {
        type: DataTypes.DECIMAL,
        allowNull: false,
    },
}, {
    sequelize,
    modelName: 'Employee',
    tableName: 'Employees',
});

export { Employee };
```
### src/models/project.ts
```ts
import { Model, DataTypes } from 'sequelize';
import sequelize from '../config/database';

class Project extends Model {
    public id!: number;
    public name!: string;
    public description!: string;
    public startDate!: Date;
    public endDate!: Date;
}

Project.init({
    id: {
        type: DataTypes.INTEGER,
        autoIncrement: true,
        primaryKey: true,
    },
    name: {
        type: DataTypes.STRING,
        unique: true,
        allowNull: false,
    },
    description: {
        type: DataTypes.STRING,
    },
    startDate: {
        type: DataTypes.DATE,
    },
    endDate: {
        type: DataTypes.DATE,
    },
}, {
    sequelize,
    modelName: 'Project',
    tableName: 'Projects',
});

export { Project };
```
### src/models/task.ts
```ts
import { Model, DataTypes } from 'sequelize';
import sequelize from '../config/database';

class Task extends Model {
    public id!: number;
    public title!: string;
    public description!: string;
    public status!: string;
    public dueDate!: Date;
}

Task.init({
    id: {
        type: DataTypes.INTEGER,
        autoIncrement: true,
        primaryKey: true,
    },
    title: {
        type: DataTypes.STRING,
        allowNull: false,
    },
    description: {
        type: DataTypes.STRING,
    },
    status: {
        type: DataTypes.STRING,
        allowNull: false,
    },
    dueDate: {
        type: DataTypes.DATE,
    },
}, {
    sequelize,
    modelName: 'Task',
    tableName: 'Tasks',
});

export { Task };
```