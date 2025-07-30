# Standard of Procedure - Backend development

## Preface

Team,

This document refers to our structure of developing our backend apps, like mobile APIs, admin panel and various services offered by ***NimbleAppgenie***.
This document ensure developers follows the structure of our project development and ensures smooth development experience without any hassles to other developers and app developers.

## Requirements

- Follow REST API Standards for request and response,
- Maintain versioning of APIs for future scopes of project,
- Optimize API requests by adding `"types"` in the request,
- Response structure:
  - Response shall adhere the HTTP status code. Here are list of most common used in our projects,
    - 200 (Ok)
    - 201 (Created)
    - 400 (Bad Request)
    - 401 (Unauthenticated) `has to use for unauthenticated response, so refresh token can be fetched`
    - 404 (Not found)
    - 403 (Forbidden)
    - 500 (Server error)
  - For APIs, we have to follow 2 types of structure, each response shall have mandatory status and message, data in the `result` key as exception, either require or not.
    1. Simple response

        ```json
            {
                "status": true, // boolean
                "message": "" // string
            }
        ```

    2. Data response

        ```json
            {
                "status": true, // boolean
                "result": {}, // array ([]) or object ({})
                "message": "" // string
            }
        ```

  - If result's list doesn't have any data, then it shall return empty.
  - No `null` shall be returned in the response. Either empty object, empty array or empty string. For boolean, it shall return false.
  - Response under the result key might get modified according to the requirement of the screen.
  - If any data consists image or has more records than unusual, it shall be paginated.
- Database Structure
  - Database shall follow this structure,
    - Table names shall be in snake_case, written as plural noun, e.g. `users`, `payments`, `contents`, `email_templates`, etc.
    - Model related to the table shall be in singular noun, in PascalCase
    - Enums shall be written in MACRO_CASE, e.g. `PUBLISHED` or `IN_TRANSIT`
    - Slugs related to webpages or any keys shall be in kebab-case
    - If the data is returned in API, and any details can be accessed by it's type, the primary for such has to be UUID.
    - Names of column shall be in camelCase. e.g. `fullName`, `createdAt`, `updatedAt`, etc.,
- Authentication
  - For PHP projects, SPA based authentication shall be implemented, hence [Sanctum](https://laravel.com/docs/sanctum) shall be used.
  - For Node JS projects, [JWT](https://www.npmjs.com/package/jsonwebtoken) shall be implemented, in which the token shall not return the User ID. The authentication process need to have a work around to fetch user indirectly.
- Code structure
  - In Laravel projects, we shall follow the structure as it is, with a Dependency Injection based approach, where we create service for common functionalities and use them accross the controllers.
  - In NodeJS projects, we follow 2 kinds of structure, `Monolithic` and `Micro-Service` based structure.
    - To utilize databases, we shall use [Sequelize ORM](https://sequelize.org/docs/v6/), or any better ORM as per required performance
    - To utilize MongoDB, we shall use [Mongoose](https://mongoosejs.com/docs/)
  - Databases shall be managed by migrations. Please visit [Laravel](https://laravel.com/docs/10.x/migrations) and [Sequelize](https://sequelize.org/docs/v6/other-topics/migrations/) approach for the migrations and seeder. Any static data shall be inserted through seeders. Visit same documentations for seeders in [Laravel](https://laravel.com/docs/seeding) and [Sequelize](https://sequelize.org/docs/v6/other-topics/migrations/#creating-the-first-seed)
- Admin Management
  - Laravel project offers frontend in itself, so admin shall be developed in the same project
  - For Node JS projects, an separate admin panel shall be developed in [react js](https://react.dev/learn) or any JS framework if client mentions requirement for admin panel in another JS framework
  - For React, we leverage to use [Vite](https://vite.dev/guide/#scaffolding-your-first-vite-project) for faster build time and Server Side Rendering (SSR) if required.
  - Design for the template of your choice, but we prefer to be constant with the admin development. Template/schema will be shared soon.
