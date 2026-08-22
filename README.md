Currency Converter and History API

A Java and Spring Boot REST API designed to retrieve official exchange rates, convert monetary values, and provide currency history for a selected period. The project uses data from the PTAX service of the Central Bank of Brazil.

Educational project created to practice REST API integration and the Strategy, Facade, and Singleton design patterns. The project is currently under development.

Project Overview

External financial APIs often expose complex parameters and data structures. This project provides a simpler interface for consulting and using official exchange-rate information.

The API is designed to:

List supported currencies.

Retrieve buy and sell exchange rates by date.

Convert Brazilian reais into a foreign currency.

Convert a foreign currency into Brazilian reais.

Retrieve currency history between two dates.

Standardize dates, monetary values, errors, and JSON responses.

The exchange rates are provided for educational and informational purposes. They may differ from the final rates used by banks or exchange companies.

Technologies

Java 21

Spring Boot

Spring Web

Jakarta Bean Validation

Springdoc OpenAPI / Swagger

Maven

JUnit

Mockito

Central Bank of Brazil PTAX API

Design Patterns

Strategy

Each conversion rule is represented by a separate strategy. This avoids large conditional blocks and makes it easier to add new conversion types.

Planned implementations:

BrlToForeignCurrencyStrategy

ForeignCurrencyToBrlStrategy

ForeignCurrencyToForeignCurrencyStrategy - future evolution

Facade

The CurrencyFacade provides a single entry point for the conversion workflow. It coordinates validation, quotation retrieval, strategy selection, calculation, and response creation.

Singleton

Spring components such as @Service, @Component, and @RestController use singleton scope by default. The HTTP client is also planned as a reusable shared bean, so a manual getInstance() implementation is unnecessary.

Application Flow

Client or Swagger
       |
       v
CurrencyController
       |
       v
CurrencyFacade
       |
       v
Services and Conversion Strategies
       |
       v
BCB PTAX Client
       |
       v
Central Bank of Brazil PTAX API

Planned Features

Retrieve currencies supported by the PTAX service.

Retrieve buy and sell quotations by currency and date.

Convert BRL to a foreign currency using the sell rate.

Convert a foreign currency to BRL using the buy rate.

Retrieve ordered exchange-rate history.

Handle weekends, holidays, and dates without quotations.

Optionally search for the latest available business day.

Return standardized HTTP errors.

Document and test endpoints with Swagger.

Main Endpoints

Method

Endpoint

Description

GET

/api/v1/currencies

Lists supported currencies

GET

/api/v1/quotations/{currency}?date=YYYY-MM-DD

Retrieves a quotation for a date

POST

/api/v1/conversions

Converts a monetary value

GET

/api/v1/history/{currency}?start=YYYY-MM-DD&end=YYYY-MM-DD

Retrieves quotation history

GET

/actuator/health

Checks application health - optional

Conversion Rules

BRL to a foreign currency

converted value = value in BRL / sell rate

Foreign currency to BRL

converted value = foreign currency value x buy rate

All monetary calculations should use BigDecimal with explicit scale and rounding. The project does not use double for financial calculations.

Example Conversion Request

POST /api/v1/conversions
Content-Type: application/json

{
  "sourceCurrency": "BRL",
  "targetCurrency": "USD",
  "amount": 1000.00,
  "date": "2026-08-21",
  "useLastBusinessDay": true
}

Example Response Structure

{
  "sourceCurrency": "BRL",
  "targetCurrency": "USD",
  "originalAmount": 1000.00,
  "convertedAmount": 0.00,
  "exchangeRate": 0.0000,
  "rateType": "SELL",
  "requestedDate": "2026-08-21",
  "quotationDate": "2026-08-21",
  "source": "Central Bank of Brazil - PTAX"
}

The zero values above are format placeholders. The application should fill them with values returned by the official source.

Dates Without Quotations

The PTAX service may not return quotations for weekends and holidays. Two behaviors are planned:

Strict mode: return 404 Not Found when no quotation exists for the requested date.

Fallback mode: search backward for the latest available quotation, with a limited number of attempts.

The response must always identify both the requested date and the date actually used.

Error Response Example

{
  "timestamp": "2026-08-22T10:30:00-03:00",
  "status": 404,
  "code": "QUOTATION_NOT_FOUND",
  "message": "No USD quotation was found for the requested date.",
  "path": "/api/v1/quotations/USD"
}

Running the Project

Requirements

JDK 21

Maven or Maven Wrapper

Git

Clone the repository

git clone https://github.com/YOUR_USERNAME/currency-converter-history-api.git
cd currency-converter-history-api

Start the application

With Maven Wrapper:

./mvnw spring-boot:run

On Windows:

.\mvnw.cmd spring-boot:run

Or with a local Maven installation:

mvn spring-boot:run

Run the tests

./mvnw test

After the OpenAPI dependency is configured, Swagger should be available at:

http://localhost:8080/swagger-ui/index.html

Project Status

This repository currently documents the project structure and implementation plan. Features will be marked as completed as they are developed and tested.

Roadmap

Create the Spring Boot project structure.

Create domain objects and validated DTOs.

Implement the Central Bank PTAX client.

Implement quotation and history services.

Implement conversion strategies.

Implement the Facade.

Create REST controllers and global error handling.

Add Swagger documentation.

Add unit and integration tests.

Add request examples and screenshots.

Add foreign-currency-to-foreign-currency conversion.

Add caching and resilience mechanisms.

Learning Goals

Consume and map data from an external REST API.

Apply Strategy, Facade, and Singleton patterns in a practical project.

Perform monetary calculations safely with BigDecimal.

Design stable request and response contracts.

Handle unavailable external services and invalid input.

Create automated tests without depending on a live external API.

Official Data Source

Central Bank of Brazil PTAX Documentation

Central Bank of Brazil Open Data Portal

Spring Boot

Author

Developed as an educational Java and Spring Boot portfolio project.
