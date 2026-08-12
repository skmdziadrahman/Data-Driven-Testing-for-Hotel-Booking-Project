<img width="565" height="592" alt="image" src="https://github.com/user-attachments/assets/8173fe3e-3bd2-40fb-965f-533f495e7ad3" />

# Data-Driven-Testing-for-Hotel-Booking-Project
Postman API automation project demonstrating data-driven testing of a hotel booking workflow using CSV, JavaScript, Newman, and GitHub Actions.

# Data Driven Testing for Hotel Booking Project

![Postman](https://img.shields.io/badge/Postman-API%20Testing-FF6C37?logo=postman\&logoColor=white)
![Newman](https://img.shields.io/badge/Newman-CLI%20Runner-00A98F)
![JavaScript](https://img.shields.io/badge/JavaScript-Test%20Scripts-F7DF1E?logo=javascript\&logoColor=black)
![CSV](https://img.shields.io/badge/CSV-Data%20Driven%20Testing-217346)
![GitHub Actions](https://img.shields.io/badge/GitHub%20Actions-CI-2088FF?logo=githubactions\&logoColor=white)

A Postman API automation project demonstrating **data-driven testing (DDT)** for a hotel booking workflow using the public ** RESTful Booker API**.

The project executes booking scenarios with multiple CSV test-data rows and validates the complete booking lifecycle through automated Postman assertions and Newman CLI execution.

## Project Objectives

This project demonstrates how to:

* Automate REST API testing with Postman
* Execute the same workflow with multiple CSV data sets
* Manage reusable values with Postman environment variables
* Validate status codes, response time, response size, JSON format, and response data
* Create and retrieve hotel bookings
* Generate and validate authentication tokens
* Perform full and partial booking updates
* Delete bookings and verify that deleted resources can no longer be retrieved
* Execute the collection from the command line with Newman
* Generate HTML execution reports
* Run automated API tests in GitHub Actions

## System Under Test

**API:** Restful Booker
**Base URL:** `https://restful-booker.herokuapp.com`

## Test Workflow

The Postman collection contains the following request flow:

1. **BookingIDs** — retrieves available booking IDs.
2. **CreateBooking** — creates a booking using data supplied by the CSV file.
3. **GetCreatedBooking** — retrieves the newly created booking and validates its values.
4. **TokenCreate** — generates an authentication token.
5. **UpdateBooking** — performs a complete booking update.
6. **GetUpdatedBooking** — verifies the updated booking.
7. **PartialUpdateBooking** — updates the booking partially.
8. **GetPartialUpdatedBooking** — verifies the partial update.
9. **DeleteBooking** — deletes the created booking.
10. **GetDeletedBooking** — confirms the deleted booking returns `404 Not Found`.

## Data-Driven Test Data

The project uses:

```text
data/Dataset_QA.csv
```

as the Newman iteration-data file.

Current CSV fields:

| Field             | Purpose                        |
| ----------------- | ------------------------------ |
| `firstname`       | Guest first name               |
| `lastname`        | Guest last name                |
| `totalprice`      | Booking price                  |
| `depositpaid`     | Deposit status                 |
| `checkin`         | Check-in date                  |
| `checkout`        | Check-out date                 |
| `additionalneeds` | Additional booking requirement |

The included dataset contains five test-data rows, allowing the complete collection workflow to execute once for each dataset.

## Project Structure

```text
data-driven-testing-hotel-booking-project/
├── .github/
│   └── workflows/
│       └── newman-tests.yml
├── data/
│   └── Dataset_QA.csv
├── postman/
│   ├── DDT_HotelBooking.postman_collection.json
│   └── DDT_Hotel_Booking.postman_environment.json
├── reports/
│   └── .gitkeep
├── .gitignore
├── package.json
└── README.md
```

## Prerequisites

Install:

* Node.js
* npm
* Postman
* Git

Verify the installations:

```bash
node --version
npm --version
git --version
```

## Installation

Clone the repository:

```bash
git clone https://github.com/YOUR-USERNAME/Data-Driven-Testing-for-Hotel-Booking-Project.git
```

Open the project:

```bash
cd Data-Driven-Testing-for-Hotel-Booking-Project
```

Install dependencies:

```bash
npm install
```

## Run the Tests with Newman

Run the complete data-driven test suite:

```bash
npm test
```

Equivalent Newman command:

```bash
npx newman run postman/DDT_HotelBooking.postman_collection.json \
  -e postman/DDT_Hotel_Booking.postman_environment.json \
  -d data/Dataset_QA.csv
```

## Generate an HTML Report

Run:

```bash
npm run test:report
```

The HTML report will be generated at:

```text
reports/newman-report.html
```

> Generated HTML reports are ignored by Git by default because runtime reports can contain request/response information. Publish only sanitized reports or screenshots where appropriate.

## Assertions Covered

The collection contains validations covering:

* HTTP status codes
* API response times
* API response sizes
* JSON response format
* Booking ID availability
* First name
* Last name
* Total booking price
* Deposit-paid status
* Check-in date
* Check-out date
* Additional booking needs
* Authentication token existence
* Authentication token data type
* Delete response validation
* `404 Not Found` validation after deletion

## Environment Variables

The Postman environment contains reusable variables such as:

| Variable       | Usage                                     |
| -------------- | ----------------------------------------- |
| `base_url`     | Restful Booker API base URL               |
| `My_Booking`   | Stores the dynamically created booking ID |
| `auth_token`   | Stores the generated authentication token |
| `FName`        | Current first name                        |
| `LName`        | Current last name                         |
| `CPrice`       | Current booking price                     |
| `TDepositPaid` | Current deposit status                    |
| `CInDate`      | Current check-in date                     |
| `COutDate`     | Current check-out date                    |
| `ANeeds`       | Current additional needs                  |

Dynamic values are populated during collection execution.

## Continuous Integration

This project includes a GitHub Actions workflow:

```text
.github/workflows/newman-tests.yml
```

The API automation suite runs automatically when:

* Code is pushed to the `main` branch
* A pull request is opened against `main`

This helps detect API automation failures before changes are merged.

## Test Reporting

Recommended test evidence for the repository:

* Newman CLI execution result
* Newman HTML report summary
* Postman collection execution screenshot
* Passing GitHub Actions workflow

## Known Issue in the Supplied Baseline

The original supplied Newman execution report contains status-code assertion mismatches for:

* `CreateBooking`
* `TokenCreate`
* `UpdateBooking`
* `PartialUpdateBooking`

In those executions, the API returned HTTP `200`, while the corresponding tests expected `201`.

The affected assertions should therefore be reviewed and corrected before publishing a final passing execution report.

## Technologies Used

* Postman
* JavaScript
* Newman
* Newman HTML Extra Reporter
* CSV
* Node.js
* npm
* Git
* GitHub
* GitHub Actions

## Key Learning Outcomes

This project demonstrates practical experience with:

* REST API automation
* Postman collection development
* Postman environment management
* Pre-request scripts
* Postman test scripts
* JavaScript assertions
* Dynamic environment variables
* Data-driven testing
* CRUD API validation
* Authentication testing
* Newman command-line execution
* Automated HTML reporting
* Continuous Integration with GitHub Actions

## Author

**Sk Md Ziad Rahman**

QA Portfolio Project

## Acknowledgement

This project uses the public RESTful Booker API as the system under test for portfolio purposes.

