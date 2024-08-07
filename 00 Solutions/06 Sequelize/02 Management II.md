### Use the setup solution of Management I

### migrations/20240730082739-delete-models
```js
'use strict';

module.exports = {
  up: async (queryInterface, Sequelize) => {
    await queryInterface.dropTable('employees');
    await queryInterface.dropTable('projects');
  },

  down: async (queryInterface, Sequelize) => {
    await queryInterface.createTable('employees', {
      id: {
        type: Sequelize.INTEGER,
        autoIncrement: true,
        primaryKey: true,
      },
      name: {
        type: Sequelize.STRING,
        allowNull: false,
      },
      // Add other fields here
    });

    await queryInterface.createTable('projects', {
      id: {
        type: Sequelize.INTEGER,
        autoIncrement: true,
        primaryKey: true,
      },
      title: {
        type: Sequelize.STRING,
        allowNull: false,
      },
      // Add other fields here
    });
  }
};
```

### migrations/20240730082752-update-model.js
```js
'use strict';

module.exports = {
  up: async (queryInterface, Sequelize) => {
    // Modify the 'tasks' table schema here
    await queryInterface.changeColumn('tasks', 'dueDate', {
      type: Sequelize.DATE,
      allowNull: false, // or any other modifications
    });
  },

  down: async (queryInterface, Sequelize) => {
    // Revert the modifications made in the up function
    await queryInterface.changeColumn('tasks', 'dueDate', {
      type: Sequelize.DATE,
      allowNull: true,
    });
  }
};
```