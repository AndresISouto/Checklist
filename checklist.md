🏗️ 1. System Design & Architecture
Before a single line of code is written.

[ ] Scalability: Have we identified the system's bottlenecks? (Is it CPU-bound, I/O-bound, or memory-bound?)

[ ] SPOF (Single Point of Failure): If any single service, database, or cloud provider goes down, what happens to the rest of the application?

[ ] State Management: Is the application stateless? If state is required (sessions, multi-step processes), where does it live?

[ ] API Contract: Are the API endpoints, payloads, and status codes explicitly agreed upon by both frontend and backend teams?

[ ] Data Flow: Is data flowing synchronously (REST/GraphQL) or asynchronously (Event-driven/Message Queues)?

[ ] Third-Party Dependencies: What external APIs are we relying on, and what is our fallback if they fail or rate-limit us?

🎨 2. UI/UX Design & Frontend Integration
Ensuring the interface is robust, accessible, and user-friendly.

[ ] Component States: Have we built states for Loading, Empty, Success, and Error/Failure?

[ ] Accessibility (a11y): Does the UI meet WCAG guidelines? (Keyboard navigation, proper aria- attributes, high color contrast).

[ ] Responsiveness: Tested on mobile, tablet, desktop, and ultra-wide screens.

[ ] Cross-Browser Compatibility: Tested on Chrome, Safari, Firefox, and Edge.

[ ] User Input Validation: Are forms validated on the client side before sending requests to the backend (immediate feedback)?

[ ] Font/Asset Loading: Are fonts and large images optimized to prevent layout shifts (CLS - Cumulative Layout Shift)?

💻 3. Frontend Development
Code quality and performance on the client side.

[ ] State Splitting: Is global state being used only when necessary, or can it be handled locally to prevent unnecessary re-renders?

[ ] Bundle Size: Checked the production bundle size. Are we lazy-loading/code-splitting heavy routes or components?

[ ] Offline Resilience: What happens if the user loses internet connection mid-session?

[ ] SEO & Meta Tags: Are Open Graph tags, meta descriptions, and semantic HTML structured correctly for web crawlers?

[ ] Local Storage/Session Cleanup: Are we clearing out temporary browser data when it’s no longer needed?

⚙️ 4. Backend Development
Business logic, resilience, and API integrity.

[ ] Idempotency: If a client retries a request (e.g., a payment or resource creation) due to a timeout, does the backend handle it without duplicating data?

[ ] Rate Limiting: Is there protection against brute-force attacks or API scraping?

[ ] Graceful Degradation: If a non-essential background service fails, does the core backend API still function?

[ ] Error Payload Standardization: Do all error responses follow a strict schema (e.g., { error: "CODE", message: "Human readable" })?

[ ] Background Processing: Are long-running tasks (sending emails, processing images) offloaded to a queue rather than blocking the HTTP response?

🗄️ 5. Database & Storage
Data integrity, speed, and lifecycle.

[ ] Indexing: Are the columns used in WHERE, JOIN, and ORDER BY clauses properly indexed? Are there too many indexes slowing down writes?

[ ] Migrations (Rollback Plan): Does every database migration have an automated, tested rollback script?

[ ] Connection Pooling: Is the backend managing database connections efficiently, or will a spike in traffic exhaust the pool?

[ ] N+1 Query Prevention: Have we checked that the ORM isn't making 100 database queries for a list of 100 items?

[ ] Data Retention & Soft Deletes: Are we permanently deleting rows, or using soft deletes (deleted_at)? What is the archival policy for old data?

🔒 6. Security & Compliance
Protecting data and infrastructure.

[ ] OWASP Top 10: Checked against SQL injection, XSS, CSRF, and broken object-level authorization.

[ ] Secrets Management: Ensure zero API keys, passwords, or certificates are hardcoded. Are they stored in an environment secret manager?

[ ] CORS Policy: Is Cross-Origin Resource Sharing configured strictly to allow only trusted domains?

[ ] Encryption: Is data encrypted in transit (HTTPS/TLS) and at rest (database encryption)?

[ ] Least Privilege: Does the application infrastructure have only the bare minimum permissions required to run?

[ ] Dependency Vulnerabilities: Have dependencies been audited for known vulnerabilities (npm audit, snyk, dependabot)?

[ ] Private info:Users can only view their own data?

🧪 7. Testing & QA
Verifying code before it leaves your machine.

[ ] Happy Path: Unit and integration tests cover the expected user behavior.

[ ] Edge Cases: Testing with null values, empty strings, massive payloads, and invalid data types.

[ ] Mocking External APIs: Are unit tests decoupled from live third-party APIs using mocks?

[ ] End-to-End (E2E): Critical user paths (Signup, Checkout, Auth) are covered by an E2E framework (Playwright/Cypress).

[ ] Regression: Did this new feature break any existing, seemingly unrelated features?

🚀 8. Deployment & DevOps (CI/CD)
Shipping code safely to production.

[ ] Environment Parity: Are staging and production environments identically configured (aside from scale and credentials)?

[ ] Zero-Downtime Strategy: Are we deploying via Blue-Green, Canary, or Rolling updates?

[ ] Health Checks: Is there a /healthz or /live endpoint that the load balancer can ping to verify the app is ready for traffic?

[ ] Build Cache Optimization: Is the Dockerfile or CI pipeline leveraging caching to make builds fast?

[ ] Feature Flags: Can this feature be deployed silently behind a flag and turned on without requiring a new deployment?

⚡ 9. Performance & Optimization
Making it fast and lightweight.

[ ] Caching Layer: Are static or slow-changing database queries cached in memory (Redis/Memcached)?

[ ] CDN Usage: Are assets (JS, CSS, images, videos) served via a Content Delivery Network?

[ ] Payload Compression: Is Gzip or Brotli compression enabled on the web server?

[ ] Memory Leaks: Checked for unclosed database connections, uncleaned event listeners, or growing memory loops.

[ ] Check the performance monitorization of pages and api calls

📊 10. Monitoring, Observability & Analytics
Knowing what’s happening in production.

[ ] Structured Logging: Are logs emitted in a structured format (like JSON) so they can be easily queried in systems like ELK or Datadog?

[ ] Alerting Thresholds: Are alerts set up for anomalous 5xx error spikes, high CPU, or memory saturation?

[ ] APM Tracing: Is Distributed Tracing active so we can trace a request from the frontend, through the backend, to the database?

[ ] Business Analytics: Are user tracking events (Amplitude, Mixpanel, Google Analytics) firing accurately without slowing down the UI thread?

📝 11. Documentation & Handover
Ensuring the next engineer (or future you) can understand it.

[ ] The "Local Setup" Test: Can a brand-new engineer clone the repo and run it locally in under 10 minutes using the README?

[ ] API Documentation: Is the API documented automatically using Swagger/OpenAPI or Postman collections?

[ ] Architecture Diagrams: Is there a visual chart (Mermaid.js, Miro) explaining how the data flows between components?

[ ] Runbooks: If an alert goes off at 3 AM for this specific feature, is there a document explaining how to debug or mitigate it?

🌍 12. Internationalization (i18n) & Localization (l10n)
Preparing your application for a global audience.

[ ] Hardcoded Strings: Ensure zero user-facing text is hardcoded in components. All strings must pull from language JSON/translation files.

[ ] Dynamic Layouts: Does the UI break if a German word is three times longer than the English version? (Use Flexbox/Grid safely).

[ ] RTL (Right-to-Left) Support: If targeting Arabic or Hebrew markets, does the layout mirror correctly?

[ ] Formatting Locales: Are dates, times, currencies, and numbers formatted using the user's browser locale (e.g., Intl.DateTimeFormat in JS)?

[ ] Timezone Agnosticism: Is all time stored in the database as UTC and only converted to local time on the user's device?

🛡️ 13. Data Privacy & Legal Compliance
Staying out of legal trouble (GDPR, CCPA, HIPAA).

[ ] Cookie Consent: Is there a compliant cookie banner that actually blocks tracking scripts before the user gives consent?

[ ] Right to be Forgotten: Is there a clear script or process to completely purge or anonymize a user’s data if they request account deletion?

[ ] PII Data Masking: Are Personally Identifiable Information (PII) like emails, phone numbers, and credit cards masked or redacted in application logs?

[ ] Data Portability: Can a user export all of their personal data in a structured format (like JSON or CSV)?

💰 14. Billing, Subscriptions & Monetization
Ensuring cash flows smoothly and securely.

[ ] Webhook Idempotency: If your payment gateway (e.g., Stripe) sends a duplicate webhook for a successful payment, does your backend handle it without upgrading the user twice?

[ ] SCA (Strong Customer Authentication): Does your checkout flow handle 3D Secure / multi-factor authentication triggers from European banks?

[ ] Grace Periods: What happens to a user's access the exact moment a subscription payment fails? Is there a retry/grace period logic?

[ ] Invoice Generation: Are legal tax requirements (like VAT calculation based on user location) handled correctly?

🛠️ 15. Technical Debt & Refactoring
Keeping the codebase maintainable long-term.

[ ] Dead Code Elimination: Have unused components, functions, and old dependencies been completely ripped out?

[ ] Deprecation Warnings: If you are changing an internal API, did you mark the old one as @deprecated to warn your teammates?

[ ] Boy Scout Rule: Did you leave the code you touched slightly cleaner than you found it?
