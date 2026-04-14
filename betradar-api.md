Prompt:

You are a senior iGaming Product Owner + Sportsbook Integration Analyst + Technical Delivery Manager with deep experience in sportsbook feed integrations, PAM systems, settlement workflows, and multi-market rollout planning.

Use the following real project context and create a complete technical integration package for AdmiralBet.

Context
I am a Product Owner at AdmiralBet and have led end-to-end sportsbook feed integrations for Betradar, Exefeed, and Innbets across multiple markets, including Serbia, Croatia, Montenegro, Bosnia & Herzegovina, Nigeria, and Uganda. My first sportsbook integration rollout took 3 months, and I later optimized the delivery model so subsequent rollouts could be completed in 2 months through better process definition, stronger coordination with development, and improved post-launch support around offer correctness and settlement flows.

I also have strong hands-on knowledge of the Betradar / NSoft environment, including live sportsbook functionality, backend logic, and operational behavior.

For this exercise, assume:

We are integrating sportsbook feed data into AdmiralBet’s PAM system

Authentication should use JWT

Target rollout timeline is 2 months

Markets in scope for detailed mapping are:

Serbia

Nigeria

Uganda

I want the output to reflect a real production integration handoff between product, backend, QA, trading, and operations

Also assume a modern sportsbook integration should include:

odds and live event consumption

settlement reconciliation

response validation

rate limit handling and retry logic

latency monitoring

duplicate event protection

market-specific validation rules

Your task
Create a detailed technical integration specification for:

Betradar sportsbook feed integration into AdmiralBet PAM

Postman test suite for Exefeed integration

Debug and fix plan for Innbets “Settlement mismatch” issue on parlay tickets

Deliverables
Provide the output in the exact structure below:

1. Integration overview
Write:

business goal

technical goal

rollout objective

why this can be delivered in 2 months based on prior rollout optimization

Include a short timeline rationale comparing:

first rollout = 3 months

optimized rollout = 2 months

2. Betradar integration architecture
Describe the end-to-end architecture for feeding sportsbook data from Betradar into AdmiralBet PAM.

Include:

source systems

middleware/integration layer

PAM ingestion layer

settlement processing

monitoring/logging layer

Explain the role of these endpoints:

/odds

/settlements

/live-events

For each endpoint define:

purpose

request method

auth model

expected polling or push behavior

core request params

sample JSON response

retry behavior

idempotency expectations

3. Authentication spec
Define a realistic JWT-based authentication model for the integration.

Include:

token issuance flow

refresh strategy

expiry strategy

required headers

environment variables

security controls

example request and response for token generation

Also explain best practices for:

caching tokens

avoiding excess auth calls

reacting to 401 vs 429 responses

4. Data mapping
Create a detailed data mapping table from feed payload to PAM schema.

Cover at minimum:

eventId

externalEventId

marketId

outcomeId

sportId

competitionId

eventStatus

liveStatus

odds

probability

settlementStatus

ticketType

country

brand

currency

marketValidity

createdAt

updatedAt

Then include market-specific mapping notes for:

Serbia

Nigeria

Uganda

Make sure to reflect:

localization differences

market availability rules

market validation exceptions

Uganda-specific invalid market scenario handling

5. Error handling and resilience
Define a production-grade error handling strategy for:

rate limiting

invalid odds

invalid market

duplicate events

delayed settlement

latency above 500ms

stale live-event feed

malformed response payloads

For each error include:

detection rule

likely root cause

fallback behavior

retry policy

escalation path

logging fields

Use best practices such as:

exponential backoff for 429 and transient 5xx errors

no blind retries for auth failures

structured logging with endpoint, params, correlationId, and timestamp

6. Rollout plan
Create a 2-month rollout plan broken into weekly phases.

Include:

discovery

sandbox integration

field mapping

QA

market validation

UAT

launch

post-launch monitoring

Also specify:

owners by team

dependencies

main risks

entry/exit criteria per phase

7. Postman test cases for Betradar
Create a practical Postman validation pack for Betradar integration.

Include:

collection structure

environments

variables

pre-request scripts

response assertions

negative tests

monitoring setup

8. Exefeed Postman suite
Generate 15 Postman test scripts for Exefeed API integration into AdmiralBet.

Scope:

odds fetch for football player props

post-match settlement

multi-market behavior

failure scenarios

The 15 scripts must cover:

valid odds fetch

missing JWT

expired JWT

invalid market for Uganda

duplicate event id

latency above 500ms

malformed odds payload

suspended market response

empty outcome list

settlement success

settlement mismatch

duplicate settlement callback

player prop line change after fetch

event already closed

multi-selection/parlay settlement consistency

For each test case include:

test name

purpose

request

expected response

Postman test script in JavaScript

pass/fail logic

9. Innbets debug plan
For the AdmiralBet Innbets feed integration, we are getting a “Settlement mismatch” error for parlay tickets.

Provide:

likely root causes

step-by-step debug checklist

log inspection plan

reconciliation flow

edge cases to test

Focus especially on:

leg-level settlement mismatch

partial updates

result ordering problems

incorrect external-to-internal mapping

duplicate callback processing

stale odds vs final result sync

10. SQL diagnostics
Write realistic SQL queries to help investigate the settlement mismatch.

Include examples for checking:

ticket header

parlay legs

external event ids

settlement status mismatch

duplicate settlement rows

processing timestamps

odds snapshot vs final settlement snapshot

Use readable SQL with short comments.

11. Node.js sync fix
Write a practical Node.js pseudocode / implementation pattern to fix settlement synchronization.

It should include:

idempotency check

event locking or deduplication

leg-by-leg comparison

mismatch logging

retry queue for transient failures

final status update only when all parlay legs are consistent

Make it realistic for a sportsbook integration service.

12. Final recommendation
Give:

rollout recommendation

technical priority order

fastest path to stable production launch in 2 months

key KPIs for post-launch monitoring

Output rules
Write like a senior technical product owner creating a handoff for engineering, QA, trading, and operations

Be practical, not generic

Use tables where helpful

Use clean JSON examples where relevant

Use realistic sportsbook terminology

Keep all examples grounded in AdmiralBet multi-market operations

Reflect the fact that the first rollout took 3 months, and process optimization reduced later rollouts to 2 months

Add this technical realism layer:

Assume feed consumers must support idempotent processing for repeated callbacks

Assume live odds and settlements may arrive out of order and require reconciliation

Assume parlay tickets should not be fully settled until all legs are validated

Assume monitoring must track response time, error rate, duplicate messages, and settlement mismatch rate

Assume Uganda may reject certain market types available in Serbia or Nigeria due to configuration differences

Assume Postman tests should be production-oriented, not just happy-path checks
