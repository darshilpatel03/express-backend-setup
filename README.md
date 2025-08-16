Node.js + Express.js + Backend and  SQL + NoSQL Database Boilerplate

This repository provides a ready-to-use backend setup built with Node.js and Express.js.
It is designed to help developers kickstart new projects quickly with a clean, scalable, and maintainable structure.

Whether you’re building a REST API, microservice, or a full-stack app backend, this boilerplate gives you a solid foundation to start with.

📂 Project Structure

```http

BACKEND/
│── controllers/     # Route handlers - business logic for APIs
│── db/              # Database configuration & connection setup
│── middleware/      # Custom middlewares (auth, logging, error handling)
│── models/          # Database models (e.g., MongoDB, Sequelize, Prisma, etc.)
│── node_modules/    # Installed dependencies (auto-generated)
│── public/          # Static files (images, docs, etc.)
│── routes/          # API route definitions
│── services/        # Reusable services (e.g., external API calls, helpers)
│── utils/           # Utility/helper functions
│── .env             # Environment variables
│── .gitignore       # Ignored files for git
│── .prettierrc      # Prettier configuration for code formatting
│── .prettierignore  # Ignore formatting on specific files
│── package.json     # Project metadata and dependencies
│── package-lock.json# Dependency lock file
│── server.js        # Entry point of the application
│── README.md        # Project documentation

```

⚡ Getting Started
1️⃣ Clone the Repository

```http
git clone https://github.com/your-username/express-backend-boilerplate.git
cd express-backend-boilerplate
```

2️⃣ Install Dependencies

```http
npm install
```

3️⃣ Configure Environment Variables
Create a .env file in the root directory and add your environment variables:

```http
PORT=5000
DB_URI=mongodb://localhost:27017/mydb   # For MongoDB
DB_HOST=localhost                       # For SQL
DB_USER=root
DB_PASS=password
DB_NAME=mydb
JWT_SECRET=your-secret-key
```
4️⃣ Start the Server

```http
npm start
```


Now your backend should be running on 👉 http://localhost:5000

🛠️ How to Use This Boilerplate

You can build your backend by following these guidelines:

Controllers → Write the business logic for your API endpoints here.

Routes → Define endpoints and link them with controllers.

Models → Create database schemas/models (e.g., User.js, Product.js).

Middleware → Implement request handling logic (e.g., authentication, logging).

Services → Place reusable logic like email services, external API calls.

Utils → Helper functions (e.g., formatDate.js, generateToken.js).

DB → Keep your database connection setup here.

🗄️ Database Setup
🔹 MongoDB (Mongoose)

Install Mongoose

```http
npm install mongoose
```

db/mongo.js

```http
const mongoose = require("mongoose");

const connectDB = async () => {
  try {
    await mongoose.connect(process.env.DB_URI, {
      useNewUrlParser: true,
      useUnifiedTopology: true,
    });
    console.log("✅ MongoDB connected successfully");
  } catch (error) {
    console.error("❌ MongoDB connection error:", error.message);
    process.exit(1);
  }
};

module.exports = connectDB;
```

models/User.js

```http

const mongoose = require("mongoose");

const userSchema = new mongoose.Schema({
  name: { type: String, required: true },
  email: { type: String, required: true, unique: true },
  password: { type: String, required: true },
}, { timestamps: true });

module.exports = mongoose.model("User", userSchema);
```


🔹 SQL (Sequelize)

Install Sequelize + Driver (example: MySQL)

```http
npm install sequelize mysql2
```

db/sql.js

```http
const { Sequelize } = require("sequelize");

const sequelize = new Sequelize(
  process.env.DB_NAME,
  process.env.DB_USER,
  process.env.DB_PASS,
  {
    host: process.env.DB_HOST,
    dialect: "mysql", // or 'postgres', 'sqlite', 'mssql'
  }
);

const connectDB = async () => {
  try {
    await sequelize.authenticate();
    console.log("✅ SQL Database connected successfully");
  } catch (error) {
    console.error("❌ SQL connection error:", error.message);
    process.exit(1);
  }
};

module.exports = { sequelize, connectDB };
```

models/User.js

```http
const { DataTypes } = require("sequelize");
const { sequelize } = require("../db/sql");

const User = sequelize.define("User", {
  name: {
    type: DataTypes.STRING,
    allowNull: false,
  },
  email: {
    type: DataTypes.STRING,
    allowNull: false,
    unique: true,
  },
  password: {
    type: DataTypes.STRING,
    allowNull: false,
  },
}, { timestamps: true });

module.exports = User;
```

📦 Scripts

npm start → Start the server

npm run dev → Start with nodemon (auto-restart on file changes)

npm run lint → Run linter (if configured)

npm run format → Format code using Prettier

🤝 Contributing

Contributions are welcome! 🎉
If you’d like to improve this boilerplate:

Fork the repository

Create a new branch (feature/your-feature)

Commit your changes

Push the branch

Open a Pull Request

📜 License

This project is licensed under the MIT License – feel free to use it for personal and commercial projects.

👉 With this setup, you can save time on repetitive tasks and start coding your backend logic right away!
