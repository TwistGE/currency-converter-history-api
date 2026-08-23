<div align="center">

<h1>🎙️ AI Voice Budget API</h1>

<p>
An intelligent personal budgeting API developed with Java, Spring Boot and Spring AI.
</p>

<p>
  <img src="https://img.shields.io/badge/Java-25-orange" alt="Java 25">
  <img src="https://img.shields.io/badge/Spring_Boot-4.0-brightgreen" alt="Spring Boot">
  <img src="https://img.shields.io/badge/Spring_AI-2.0-green" alt="Spring AI">
  <img src="https://img.shields.io/badge/MySQL-9.6-blue" alt="MySQL">
  <img src="https://img.shields.io/badge/Docker-Compose-blue" alt="Docker">
  <img src="https://img.shields.io/badge/Status-In_Development-yellow" alt="Status">
</p>

</div>

<hr>

<h2>📖 About the Project</h2>

<p>
AI Voice Budget API is an intelligent financial assistant that processes voice
commands related to personal expenses.
</p>

<p>
The user can send an audio command such as:
</p>

<blockquote>
“I spent 80 reais at the grocery store.”
</blockquote>

<p>
The application transcribes the audio, identifies the user's intention,
executes the correct financial operation, stores the transaction in MySQL
and generates an audio confirmation.
</p>

<p>
This is an educational project developed as part of the DIO Java and
Spring Boot learning track.
</p>

<h2>🎯 Project Goals</h2>

<ul>
  <li>Register expenses using voice commands.</li>
  <li>Transform natural language into financial operations.</li>
  <li>Store transactions in a relational database.</li>
  <li>Consult expenses by category.</li>
  <li>Generate audio confirmations.</li>
  <li>Apply Spring AI Tool Calling in a real application.</li>
  <li>Practice Clean Architecture and Domain-Driven Design concepts.</li>
</ul>

<h2>🔄 Application Flow</h2>

<pre>
Audio File
    ↓
Speech-to-Text
    ↓
Spring AI Chat Client
    ↓
Intent Identification
    ↓
Tool Calling
    ↓
Application Use Case
    ↓
MySQL Database
    ↓
Text-to-Speech
    ↓
MP3 Response
</pre>

<h2>✨ Main Features</h2>

<ul>
  <li>Create financial transactions through REST.</li>
  <li>List transactions by category.</li>
  <li>Receive financial commands through audio files.</li>
  <li>Convert speech into text.</li>
  <li>Use artificial intelligence to identify user intentions.</li>
  <li>Execute application tools through Spring AI.</li>
  <li>Persist transactions in MySQL.</li>
  <li>Generate an MP3 audio response.</li>
</ul>

<h2>🚀 Planned Portfolio Evolution</h2>

<p>
The planned improvement is a financial summary feature that allows users
to consult their expenses by period and category.
</p>

<p>Examples of supported commands:</p>

<ul>
  <li>“How much did I spend this month?”</li>
  <li>“How much did I spend on groceries between August 1 and August 15?”</li>
  <li>“Summarize my expenses by category for the last week.”</li>
</ul>

<h2>🛠️ Technologies</h2>

<table>
  <tr>
    <th>Technology</th>
    <th>Purpose</th>
  </tr>
  <tr>
    <td>Java 25</td>
    <td>Main programming language</td>
  </tr>
  <tr>
    <td>Spring Boot 4</td>
    <td>Application and REST API development</td>
  </tr>
  <tr>
    <td>Spring AI</td>
    <td>Chat, transcription, Tool Calling and text-to-speech</td>
  </tr>
  <tr>
    <td>Spring Data JPA</td>
    <td>Database persistence</td>
  </tr>
  <tr>
    <td>MySQL</td>
    <td>Transaction storage</td>
  </tr>
  <tr>
    <td>Docker Compose</td>
    <td>Local database environment</td>
  </tr>
  <tr>
    <td>Gradle</td>
    <td>Dependency management and build</td>
  </tr>
  <tr>
    <td>JUnit</td>
    <td>Automated testing</td>
  </tr>
</table>

<h2>🏗️ Architecture</h2>

<p>
The project is organized into domain, application and infrastructure layers.
</p>

<pre>
src/main/java/dio/budgeting/

├── domain/
│   ├── Category
│   ├── Transaction
│   ├── TransactionId
│   └── TransactionRepository
│
├── application/
│   ├── PersistTransactionUseCase
│   ├── ListTransactionsByCategoryUseCase
│   └── FinancialSummaryUseCase
│
└── infrastructure/
    ├── http/
    ├── persistence/
    └── springai/
</pre>

<p>
The artificial intelligence model does not access the database directly.
It selects an authorized tool, which calls an application use case responsible
for validation and persistence.
</p>

<h2>🌐 Endpoints</h2>

<table>
  <tr>
    <th>Method</th>
    <th>Endpoint</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>POST</td>
    <td><code>/transactions</code></td>
    <td>Creates a transaction from JSON</td>
  </tr>
  <tr>
    <td>GET</td>
    <td><code>/transactions/{category}</code></td>
    <td>Lists transactions by category</td>
  </tr>
  <tr>
    <td>POST</td>
    <td><code>/transactions/ai</code></td>
    <td>Processes a financial command from audio</td>
  </tr>
  <tr>
    <td>GET</td>
    <td><code>/transactions/summary</code></td>
    <td>Returns a financial summary - planned feature</td>
  </tr>
</table>

<h2>📤 Creating a Transaction</h2>

<pre><code>{
  "description": "Grocery shopping",
  "category": "GROCERIES",
  "amount": 8050
}</code></pre>

<p>
The <code>amount</code> field is stored in cents. Therefore,
<code>8050</code> represents <code>R$ 80.50</code>.
</p>

<h2>🎤 Sending an Audio Command</h2>

<pre><code>curl -X POST http://localhost:8080/transactions/ai \
  -F "file=@expense.m4a" \
  --output response.mp3</code></pre>

<h2>▶️ Running the Project</h2>

<h3>Requirements</h3>

<ul>
  <li>JDK 25</li>
  <li>Docker Desktop or Docker Engine</li>
  <li>Docker Compose</li>
  <li>Git</li>
  <li>A valid API key for the configured AI provider</li>
</ul>

<h3>Clone the repository</h3>

<pre><code>git clone https://github.com/YOUR_USERNAME/ai-voice-budget-api.git
cd ai-voice-budget-api</code></pre>

<h3>Configure the API key</h3>

<p>Linux, macOS or WSL:</p>

<pre><code>export OPENAI_API_KEY="YOUR_API_KEY"</code></pre>

<p>Windows PowerShell:</p>

<pre><code>$env:OPENAI_API_KEY="YOUR_API_KEY"</code></pre>

<p>
<strong>Important:</strong> Never publish API keys or credentials on GitHub.
</p>

<h3>Start the database</h3>

<pre><code>docker compose up -d</code></pre>

<h3>Start the application</h3>

<p>Linux, macOS or WSL:</p>

<pre><code>./gradlew bootRun</code></pre>

<p>Windows:</p>

<pre><code>.\gradlew.bat bootRun</code></pre>

<h3>Run the tests</h3>

<pre><code>./gradlew test</code></pre>

<h2>📌 Project Status</h2>

<p>
This project is currently under development. The first goal is to reproduce
the official Spring AI budgeting flow. After that, the application will receive
the financial summary feature.
</p>

<h2>🗺️ Roadmap</h2>

<ul>
  <li>⬜ Configure the project and local environment.</li>
  <li>⬜ Validate transaction creation through REST.</li>
  <li>⬜ Validate transaction queries by category.</li>
  <li>⬜ Complete the speech-to-text flow.</li>
  <li>⬜ Complete Tool Calling and persistence.</li>
  <li>⬜ Generate MP3 confirmation responses.</li>
  <li>⬜ Standardize monetary values in cents.</li>
  <li>⬜ Add transaction dates.</li>
  <li>⬜ Add financial summaries.</li>
  <li>⬜ Add automated tests.</li>
  <li>⬜ Add screenshots and request examples.</li>
</ul>

<h2>📚 Learning Goals</h2>

<ul>
  <li>Understand dependency injection with Spring.</li>
  <li>Apply use cases, repositories and adapters.</li>
  <li>Integrate AI models into a Java application.</li>
  <li>Use Spring AI Tool Calling.</li>
  <li>Process audio input and output.</li>
  <li>Persist financial information safely.</li>
  <li>Document an API for a professional portfolio.</li>
</ul>

<h2>🔗 References</h2>

<ul>
  <li>
    <a href="https://github.com/digitalinnovationone/dio-spring-boot-learning-track">
      DIO Spring Boot Learning Track
    </a>
  </li>
  <li>
    <a href="https://github.com/digitalinnovationone/dio-spring-boot-learning-track/blob/main/05-spring-ai/README.md">
      Official Spring AI Project Challenge
    </a>
  </li>
  <li>
    <a href="https://docs.spring.io/spring-ai/reference/">
      Spring AI Documentation
    </a>
  </li>
</ul>

<hr>

<div align="center">

<p>
Developed as an educational project for the DIO Java and Spring Boot learning track.
</p>

</div>
