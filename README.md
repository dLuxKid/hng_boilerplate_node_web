
# API and Database Design Documentation

This repository contains the boilerplate for an API and its corresponding database design. It includes user management, admin functionalities, organisation management, widgets, blogs, and notifications.

## Table of Contents

1. [Installation](#installation)
2. [API Documentation](#api-documentation)
3. [Database Schema](#database-schema)
4. [Authentication](#authentication)
5. [API Endpoints](#api-endpoints)
6. [Contributing](#contributing)
7. [License](#license)

## Installation

1. Clone the repository:

   ```bash
   git clone https://github.com/dLuxKid/hng_boilerplate_node_web/tree/team-kaiju
   cd hng_boilerplate_node_web
   ```

2. Follow the instructions in the backend folder's `README.md` to set up the backend.

## API Documentation

The API documentation is provided in the OpenAPI 3.0 format. You can view and interact with the API using Swagger UI or any other OpenAPI-compatible tool.

### Swagger UI

You can view the Swagger UI by serving the `swagger.json` file. Here is an example URL format:

- [Swagger UI](https://hng-task-3-mocha.vercel.app/) - Replace with your actual documentation link.

## Database Schema

The database schema is designed using `dbdiagram.io`. Below are the tables included in this project:

- **Users**: Stores user information.
- **Payment**: Logs payment details.
- **Transaction**: Logs all debits and credits.
- **Admin**: Stores admin information.
- **Waitlist**: Stores waitlist information.
- **Organisation**: Stores organization details.
- **OrganisationUser**: Links users to organizations.
- **Widget**: Stores widget information.
- **Blog**: Stores blog entries.
- **Notification**: Stores notification messages.

### dbdiagram.io Schema

You can visualize the database schema [here](https://www.dbdiagram.io/d/team-kaiju-66922c4e9939893daed256bf).

```sql
Table Users {
  user_id int [primary key, increment]
  surname varchar(255)
  other_names varchar(255)
  phone_number varchar(20)
  email varchar(255) [unique]
  password varchar(255)
  created_at timestamp [default: `now()`]
  updated_at timestamp [default: `now()`]
}

Table Payment {
  payment_id int [primary key, increment]
  payment_reference varchar(255)
  amount decimal(10, 2)
  created_at timestamp [default: `now()`]
  updated_at timestamp [default: `now()`]
  user_id int [ref: > Users.user_id]
}

Table Transaction {
  transaction_id int [primary key, increment]
  amount decimal(10, 2)
  transaction_type varchar(50)
  created_at timestamp [default: `now()`]
  updated_at timestamp [default: `now()`]
  user_id int [ref: > Users.user_id]
}

Table Admin {
  admin_id int [primary key, increment]
  email varchar(255) [unique]
  surname varchar(255)
  other_names varchar(255)
  password varchar(255)
  user_id int [ref: > Users.user_id]
  created_at timestamp [default: `now()`]
  updated_at timestamp [default: `now()`]
}

Table Waitlist {
  waitlist_id int [primary key, increment]
  email varchar(255) [unique]
  surname varchar(255)
  other_names varchar(255)
  created_at timestamp [default: `now()`]
  updated_at timestamp [default: `now()`]
}

Table Organisation {
  organisation_id int [primary key, increment]
  name varchar(255)
  description varchar
  created_at timestamp [default: `now()`]
  updated_at timestamp [default: `now()`]
}

Table OrganisationUsers {
  id int [primary key, increment]
  organisation_id int [ref: > Organisation.organisation_id]
  user_id int [ref: > Users.user_id]
  role varchar(255)
  created_at timestamp [default: `now()`]
  updated_at timestamp [default: `now()`]
}


Table Widgets {
  widget_id int [primary key]
  created_by int [ref: > Users.user_id]
  name varchar
  description text
  created_at timestamp [default: `now()`]
  updated_at timestamp [default: `now()`]
}


Table Notifications {
  notification_id int [primary key]
  recipient_id int [ref: > Users.user_id]
  message text
  read bool [default: 0]
  created_at timestamp [default: `now()`]
}

Table blogs {
  blog_id int [primary key]
  published_by int [ref: > Users.user_id]
  title varchar
  content text
  published_at timestamp [default: `now()`]
}


Ref: "Notifications"."notification_id" < "Notifications"."message"
```

## Authentication

The API uses bearer token authentication for securing endpoints. Make sure to include the token in the `Authorization` header of your requests.

## API Endpoints

The API endpoints are defined as follows:

### User Endpoints

- `POST /auth/register`: Register a new user.
- `POST /auth/login`: User login.
- `GET /user/profile`: Get user profile.
- `POST /user/forgot-password`: Start forgot password process.
- `POST /user/reset-password`: Complete forgot password process.
- `POST /user/change-password`: Change password.

### Admin Endpoints

- `POST /admin/register`: Register a new admin.
- `POST /admin/login`: Admin login.

### Waitlist

- `POST /waitlist`: Register on the waitlist.
- `GET /waitlist`: Get all users on the waitlist.

### Organisation Endpoints

- `GET /organisation`: Get your organisation.
- `POST /organisation/create`: Create a new organisation.
- `POST /organisation/add-user`: Add a user to an organisation.

### Widget Endpoints

- `POST /widgets`: Create a new widget.
- `GET /widgets`: Get all widgets.

### Blog Endpoints

- `POST /blogs`: Create a new blog.
- `GET /blogs`: Get all blogs.

### Notification Endpoints

- `POST /notifications`: Create a new notification.
- `GET /notifications`: Get your notifications.

## Contributing

Contributions are welcome! Please open an issue or submit a pull request for any improvements or bug fixes.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

```

This `README.md` provides a comprehensive overview of the project, detailing the installation process, API documentation, database schema, and available API endpoints. Adjust the links and commands as necessary to fit your project's specific setup.
```
