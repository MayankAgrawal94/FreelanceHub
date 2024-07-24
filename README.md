# Job Contract Management System

The Job Contract Management System is a backend application built using Node.js and Express.js. This system simulates a platform where clients can create contracts with contractors, and contractors can perform jobs for clients. The application manages profiles, contracts, and job payments, ensuring a seamless workflow between clients and contractors.

## Key Features:

- **_Profile Management_**: Supports both client and contractor profiles, each with a balance property.

- **_Contract Handling_**: Allows creation and management of contracts with various statuses (new, in_progress, terminated).

- **_Job Management_**: Enables contractors to get paid for jobs performed under specific contracts.

- **_Payment Processing_**: Ensures clients can pay contractors based on their balance and job requirements.

- **_Administrative Insights_**: Provides endpoints to fetch top-earning professions and highest-paying clients within a specified timeframe.

This project demonstrates a robust REST API with essential functionalities for managing job contracts and payments, serving as a foundational backend for a job contracting platform.

## Data Models

> **All models are defined under src/models/_.js**

### Profile

A profile can be either a `client` or a `contractor`.
clients create contracts with contractors. contractor does jobs for clients and get paid.
Each profile has a balance property.

### Contract

A contract between and client and a contractor.
Contracts have 3 statuses, `new`, `in_progress`, `terminated`. contracts are considered active only when in status `in_progress`
Contracts group jobs within them.

### Job

contractor get paid for jobs by clients under a certain contract.

## Installation & Set Up

The exercise requires [Node.js](https://nodejs.org/en/) to be installed. I recommend using the LTS version >= 18.

1. Clone the repository:

    ```sh
    git clone https://github.com/MayankAgrawal94/Job-Contract-Management-System.git
    cd Job-Contract-Management-System
    ```

1. In the repo root directory, run `npm install` to gather all dependencies.

1. Next, `npm run seed` will seed the local SQLite database. **Warning: This will drop the database if it exists**. The database lives in a local file `database.sqlite3`.

1. Then run `npm start` which should start the server .


## Technical Notes

- The server is running with [nodemon](https://nodemon.io/) which will automatically restart for you when you modify and save a file.

- The database provider is SQLite, which will store data in a file local to your repository called `database.sqlite3`. The ORM [Sequelize](http://docs.sequelizejs.com/) is on top of it. You should only have to interact with Sequelize - **please spend some time reading sequelize documentation before starting the exercise.**

- To authenticate users use the `getProfile` middleware that is located under src/middleware/getProfile.js. users are authenticated by passing `profile_id` in the request header. after a user is authenticated his profile will be available under `req.profile`. make sure only users that are on the contract can access their contracts.
- The server is running on port 3001.

## APIs description

Below is a list of the required API's for the application.

1. **_GET_** `/contracts/:id` - This API return the contract only if it belongs to the profile calling.

1. **_GET_** `/contracts` - Returns a list of contracts belonging to a user (client or contractor), the list should only contain non terminated contracts.

1. **_GET_** `/jobs/unpaid` - Get all unpaid jobs for a user (**_either_** a client or contractor), for **_active contracts only_**.

1. **_POST_** `/jobs/:job_id/pay` - Pay for a job, a client can only pay if his balance >= the amount to pay. The amount should be moved from the client's balance to the contractor balance.

1. **_POST_** `/balances/deposit/:userId` - Deposits money into the the the balance of a client, a client can't deposit more than 25% his total of jobs to pay. (at the deposit moment)

1. **_GET_** `/admin/best-profession?start=<date>&end=<date>` - Returns the profession that earned the most money (sum of jobs paid) for any contactor that worked in the query time range.

1. **_GET_** `/admin/best-clients?start=<date>&end=<date>&limit=<integer>` - returns the clients the paid the most for jobs in the query time period. limit query parameter should be applied, default limit is 2.

```
 [
    {
        "id": 1,
        "fullName": "Reece Moyer",
        "paid" : 100.3
    },
    {
        "id": 200,
        "fullName": "Debora Martin",
        "paid" : 99
    },
    {
        "id": 22,
        "fullName": "Debora Martin",
        "paid" : 21
    }
]
```

## Contributing
If you have any suggestions or improvements, feel free to submit a pull request or open an issue.

## Contact
If you have any feedback, questions, or suggestions, feel free to reach out.
connect me at `jobs@mayankagrawal.co.in` or can DM me on [LinkedIn](https://www.linkedin.com/in/er-mayank/).
