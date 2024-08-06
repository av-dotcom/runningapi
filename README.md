# Runnerz - Run Tracking Application

Runnerz is a simple Spring Boot application for tracking running activities. Users can log runs, view run details, and manage their running records easily.

## Features

- **Log Runs**: Add new running entries with details like title, start and end times, distance, and location.
- **View Runs**: Retrieve a list of all runs or search by specific criteria.
- **Manage Runs**: Update or delete existing runs.

## Getting Started

### Prerequisites

- **Java 17** or higher
- **Spring Boot** framework

### Installation

1. **Clone the repository**:

   ```bash
   git clone https://github.com/av-dotcom/runnerz.git
   cd runnerz
   ```

2. **Set up the database**:

   Ensure you have a running instance of a database supported by Spring JDBC. Update your database credentials in the `application.properties` file.

3. **Run the application**:

   Use Maven to build and run the application:

   ```bash
   mvn clean install
   mvn spring-boot:run
   ```

   The application will start on `http://localhost:8080`.

## Usage

- **Add a Run**: Use the `/runs` endpoint to create a new run.
- **View Runs**: Access `/runs` to view all runs or `/runs/{id}` to view a specific run.
- **Update/Delete a Run**: Modify or remove run entries using the `/runs/{id}` endpoint.

## Code Overview

- **`RunRepository`**: Handles database operations for run records, using Spring JDBC for queries and updates.

```java
public List<Run> findAll() {
    return jdbcClient.sql("select * from run").query(Run.class).list();
}

public void create(Run run) {
    jdbcClient.sql("INSERT INTO Run(id, title, started_on, completed_on, miles, location) values(?,?,?,?,?,?)")
              .params(List.of(run.id(), run.title(), run.startedOn(), run.completedOn(), run.miles(), run.location().toString()))
              .update();
}
```
