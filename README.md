<div align="center">

<h1>💱 Currency Converter and History API</h1>

<p>
A Java and Spring Boot REST API for currency conversion and exchange-rate history.
</p>

<p>
  <img src="https://img.shields.io/badge/Java-21-orange" alt="Java 21">
  <img src="https://img.shields.io/badge/Spring_Boot-green" alt="Spring Boot">
  <img src="https://img.shields.io/badge/API-REST-blue" alt="REST API">
  <img src="https://img.shields.io/badge/BCB-PTAX-darkblue" alt="BCB PTAX">
  <img src="https://img.shields.io/badge/Status-In_Development-yellow" alt="Status">
</p>

</div>

<hr>

<h2>📖 About the Project</h2>

<p>
Currency Converter and History API is a REST API designed to retrieve official
exchange rates, convert monetary values and provide the exchange-rate history
of a selected currency.
</p>

<p>
The application uses official PTAX data provided by the Central Bank of Brazil.
</p>

<p>
This educational project was created to practice external API integration,
monetary calculations and the Strategy, Facade and Singleton design patterns.
</p>

<h2>🎯 Project Goals</h2>

<ul>
  <li>List currencies supported by the external source.</li>
  <li>Retrieve buy and sell exchange rates by date.</li>
  <li>Convert Brazilian reais into foreign currencies.</li>
  <li>Convert foreign currencies into Brazilian reais.</li>
  <li>Retrieve currency history between two dates.</li>
  <li>Handle weekends and dates without quotations.</li>
  <li>Apply Design Patterns in a practical Spring Boot project.</li>
</ul>

<h2>✨ Planned Features</h2>

<ul>
  <li>List currencies supported by the PTAX service.</li>
  <li>Retrieve official quotations by currency and date.</li>
  <li>Convert BRL into a foreign currency.</li>
  <li>Convert a foreign currency into BRL.</li>
  <li>Retrieve ordered exchange-rate history.</li>
  <li>Search for the latest available business day.</li>
  <li>Return standardized JSON responses.</li>
  <li>Handle invalid currencies, dates and monetary values.</li>
  <li>Provide Swagger documentation.</li>
</ul>

<h2>🛠️ Technologies</h2>

<table>
  <tr>
    <th>Technology</th>
    <th>Purpose</th>
  </tr>
  <tr>
    <td>Java 21</td>
    <td>Main programming language</td>
  </tr>
  <tr>
    <td>Spring Boot</td>
    <td>REST API development</td>
  </tr>
  <tr>
    <td>Spring Web</td>
    <td>Controllers and external API integration</td>
  </tr>
  <tr>
    <td>Jakarta Validation</td>
    <td>Request validation</td>
  </tr>
  <tr>
    <td>Springdoc OpenAPI</td>
    <td>Swagger documentation</td>
  </tr>
  <tr>
    <td>Maven</td>
    <td>Dependency and build management</td>
  </tr>
  <tr>
    <td>JUnit and Mockito</td>
    <td>Automated testing</td>
  </tr>
  <tr>
    <td>BCB PTAX API</td>
    <td>Official exchange-rate data source</td>
  </tr>
</table>

<h2>🧩 Design Patterns</h2>

<h3>Strategy</h3>

<p>
Each conversion rule is represented by a different strategy. This makes it
possible to add new conversion types without creating a large block of
conditional statements.
</p>

<ul>
  <li><code>BrlToForeignCurrencyStrategy</code></li>
  <li><code>ForeignCurrencyToBrlStrategy</code></li>
  <li><code>ForeignCurrencyToForeignCurrencyStrategy</code> - future feature</li>
</ul>

<h3>Facade</h3>

<p>
The <code>CurrencyFacade</code> provides a single entry point for the conversion
process. It coordinates validation, quotation retrieval, strategy selection,
calculation and response creation.
</p>

<h3>Singleton</h3>

<p>
Spring components annotated with <code>@Service</code>,
<code>@Component</code> and <code>@RestController</code> use singleton scope
by default. Therefore, a manual <code>getInstance()</code> implementation is
not required.
</p>

<h2>🏗️ Application Architecture</h2>

<pre>
Client or Swagger
        ↓
CurrencyController
        ↓
CurrencyFacade
        ↓
Services and Conversion Strategies
        ↓
BCB PTAX Client
        ↓
Central Bank of Brazil PTAX API
</pre>

<h2>📁 Planned Project Structure</h2>

<pre>
src/main/java/com/example/currencyconverter/

├── config/
│   └── HttpClientConfig
│
├── controller/
│   └── CurrencyController
│
├── facade/
│   └── CurrencyFacade
│
├── client/
│   ├── BcbPtaxClient
│   └── dto/
│
├── service/
│   ├── QuotationService
│   └── HistoryService
│
├── strategy/
│   ├── ConversionStrategy
│   ├── BrlToForeignCurrencyStrategy
│   └── ForeignCurrencyToBrlStrategy
│
├── domain/
│   ├── Currency
│   └── Quotation
│
├── dto/
│   ├── request/
│   └── response/
│
└── exception/
    └── GlobalExceptionHandler
</pre>

<h2>🌐 Endpoints</h2>

<table>
  <tr>
    <th>Method</th>
    <th>Endpoint</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>GET</td>
    <td><code>/api/v1/currencies</code></td>
    <td>Lists supported currencies</td>
  </tr>
  <tr>
    <td>GET</td>
    <td><code>/api/v1/quotations/{currency}?date=YYYY-MM-DD</code></td>
    <td>Retrieves a quotation for a specific date</td>
  </tr>
  <tr>
    <td>POST</td>
    <td><code>/api/v1/conversions</code></td>
    <td>Converts a monetary value</td>
  </tr>
  <tr>
    <td>GET</td>
    <td><code>/api/v1/history/{currency}?start=YYYY-MM-DD&amp;end=YYYY-MM-DD</code></td>
    <td>Retrieves quotation history</td>
  </tr>
</table>

<h2>🧮 Conversion Rules</h2>

<h3>BRL to a foreign currency</h3>

<pre>
Converted value = Value in BRL ÷ Sell rate
</pre>

<h3>Foreign currency to BRL</h3>

<pre>
Converted value = Foreign currency value × Buy rate
</pre>

<p>
All monetary calculations use <code>BigDecimal</code> with explicit scale and
rounding. The project does not use <code>double</code> for financial calculations.
</p>

<h2>📤 Example Conversion Request</h2>

<pre><code>{
  "sourceCurrency": "BRL",
  "targetCurrency": "USD",
  "amount": 1000.00,
  "date": "2026-08-21",
  "useLastBusinessDay": true
}</code></pre>

<h2>📥 Example Response</h2>

<pre><code>{
  "sourceCurrency": "BRL",
  "targetCurrency": "USD",
  "originalAmount": 1000.00,
  "convertedAmount": 0.00,
  "exchangeRate": 0.0000,
  "rateType": "SELL",
  "requestedDate": "2026-08-21",
  "quotationDate": "2026-08-21",
  "source": "Central Bank of Brazil - PTAX"
}</code></pre>

<p>
The zero values above are format placeholders. The application should replace
them with the values returned by the official PTAX service.
</p>

<h2>📅 Dates Without Quotations</h2>

<p>
The PTAX service may not provide quotations for weekends and holidays.
The application plans to support two behaviors:
</p>

<ul>
  <li>
    <strong>Strict mode:</strong> returns <code>404 Not Found</code> when no
    quotation exists for the requested date.
  </li>
  <li>
    <strong>Fallback mode:</strong> searches backward for the latest available
    quotation, with a limited number of attempts.
  </li>
</ul>

<p>
The response must identify both the requested date and the date actually used.
</p>

<h2>⚠️ Error Response Example</h2>

<pre><code>{
  "timestamp": "2026-08-22T10:30:00-03:00",
  "status": 404,
  "code": "QUOTATION_NOT_FOUND",
  "message": "No USD quotation was found for the requested date.",
  "path": "/api/v1/quotations/USD"
}</code></pre>

<h2>▶️ Running the Project</h2>

<h3>Requirements</h3>

<ul>
  <li>JDK 21</li>
  <li>Maven or Maven Wrapper</li>
  <li>Git</li>
</ul>

<h3>Clone the repository</h3>

<pre><code>git clone https://github.com/YOUR_USERNAME/currency-converter-history-api.git
cd currency-converter-history-api</code></pre>

<h3>Start the application</h3>

<p>Linux, macOS or WSL:</p>

<pre><code>./mvnw spring-boot:run</code></pre>

<p>Windows:</p>

<pre><code>.\mvnw.cmd spring-boot:run</code></pre>

<p>Using a local Maven installation:</p>

<pre><code>mvn spring-boot:run</code></pre>

<h3>Run the tests</h3>

<pre><code>./mvnw test</code></pre>

<h3>Swagger</h3>

<p>
After starting the application, the Swagger interface should be available at:
</p>

<pre><code>http://localhost:8080/swagger-ui/index.html</code></pre>

<h2>📌 Project Status</h2>

<p>
This repository currently documents the project structure and implementation
plan. Features will be marked as completed as they are developed and tested.
</p>

<h2>🗺️ Roadmap</h2>

<ul>
  <li>⬜ Create the Spring Boot project structure.</li>
  <li>⬜ Create domain objects and validated DTOs.</li>
  <li>⬜ Implement the Central Bank PTAX client.</li>
  <li>⬜ Implement quotation and history services.</li>
  <li>⬜ Implement the conversion strategies.</li>
  <li>⬜ Implement the Facade.</li>
  <li>⬜ Create REST controllers.</li>
  <li>⬜ Add global error handling.</li>
  <li>⬜ Add Swagger documentation.</li>
  <li>⬜ Add unit and integration tests.</li>
  <li>⬜ Add request examples and screenshots.</li>
  <li>⬜ Add caching and resilience mechanisms.</li>
</ul>

<h2>📚 Learning Goals</h2>

<ul>
  <li>Consume and map information from an external REST API.</li>
  <li>Apply Strategy, Facade and Singleton patterns.</li>
  <li>Perform safe monetary calculations with BigDecimal.</li>
  <li>Design stable request and response contracts.</li>
  <li>Handle invalid inputs and unavailable external services.</li>
  <li>Create automated tests without depending on a live external API.</li>
</ul>

<h2>🔗 Official Data Sources</h2>

<ul>
  <li>
    <a href="https://olinda.bcb.gov.br/olinda/servico/PTAX/versao/v1/documentacao">
      Central Bank of Brazil PTAX Documentation
    </a>
  </li>
  <li>
    <a href="https://dadosabertos.bcb.gov.br/dataset/taxas-de-cambio-todos-os-boletins-diarios">
      Central Bank of Brazil Open Data Portal
    </a>
  </li>
  <li>
    <a href="https://spring.io/projects/spring-boot">
      Spring Boot
    </a>
  </li>
</ul>

<h2>⚖️ Disclaimer</h2>

<p>
The quotations provided by this project are intended for educational and
informational purposes. They may differ from the final rates used by banks,
financial institutions or exchange companies.
</p>

<hr>

<div align="center">

<p>
Developed as an educational Java and Spring Boot portfolio project.
</p>

</div>
