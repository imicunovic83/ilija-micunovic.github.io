Prompt:

You are a senior iGaming Product Owner + Retention Marketing Specialist + Bonus Operations Lead with deep experience designing, implementing, and measuring tiered promotional schemes in regulated markets.

Use the following real project context and create a complete product specification package for AdmiralBet's tiered parlay bonus.

Context
I am/was a Product Owner at AdmiralBet and led from concept to implementation a tiered parlay bonus scheme that rewarded players based on the number of parlay legs selected:

2% bonus for 3 pairs (minimum 3 legs)

Tiered progression up to 701% bonus for 40+ pairs

Minimum odds requirement: 1.30 per leg

Maximum payout cap: 21M RSD

Wagering requirements: x5 on cash (non-bonus) tickets

This promotion was designed to drive parlay volume, retention, and deposit reactivation while maintaining responsible margins through strict min-odds and payout caps.

Markets in scope: Serbia (primary market with RSD currency and localized messaging)

Your task
Create a complete product specification package covering technical implementation, validation, A/B testing, and localized execution.

Deliverables
Provide the output in the exact structure below:

1. Product overview
Write:

business objective (parlay volume, retention, deposit reactivation)

player value proposition

commercial guardrails (min odds, payout cap, wagering reqs)

expected business impact based on industry benchmarks

2. Tiered bonus structure
Document the complete tier structure in a clear table format:

Legs	Bonus %	Min Odds/Leg	Example Bet	Bonus Amount	Max Payout
3	2%	1.30	...	...	21M RSD
...	...	...	...	...	21M RSD
40+	701%	1.30	...	...	21M RSD
Include:

calculation formulas

edge case handling (exactly 40 legs vs 41+)

rounding rules

currency conversion notes (if multi-currency)

3. Technical acceptance criteria
Create detailed acceptance criteria for the development team implementing this feature.

Cover these areas:

Bonus calculation engine

Input validation (leg count, odds per leg)

Tier lookup logic

Payout cap enforcement

Real-time calculation during bet placement

Ticket processing

Bonus addition to winning parlays

Partial cashout behavior

Void leg handling

Player balance

Bonus credit to bonus wallet

Wagering requirement tracking

Release to cash balance logic

UI/UX

Bonus preview during bet builder

Real-time tier indicator

Post-settlement bonus notification

Format as Gherkin-style acceptance criteria with Given/When/Then scenarios.

4. Wagering requirements spec
Define x5 wagering requirements implementation details:

Applies only to cash tickets (not bonus bets)

Tracking per player/promo code

Progress indicator in player dashboard

Release conditions and automation

Edge cases (multiple promos, partial wagering)

Include:

database schema additions

API endpoints needed

UI display requirements

5. SQL validation suite
Write production-ready SQL queries for:

Bonus calculation validation:

sql
-- Verify bonus calculation for sample tickets
SELECT ticket_id, legs, min_odds, calculated_bonus, actual_bonus
FROM bonus_calculation_log
WHERE created_at >= '2026-04-01'
  AND legs BETWEEN 3 AND 40
ORDER BY legs DESC;
Payout cap enforcement:

sql
-- Check 21M RSD cap compliance
SELECT player_id, SUM(bonus_amount) as total_bonus
FROM player_bonus_wallet
WHERE promo_code = 'PARLAY701'
GROUP BY player_id
HAVING total_bonus > 21000000;
Wagering progress:

sql
-- Wagering requirement fulfillment check
SELECT player_id, promo_code, 
       bonus_amount, wagered_amount, 
       (wagered_amount / (bonus_amount * 5)) as progress_pct
FROM promo_tracking;
Tier distribution analysis:

sql
-- Which tiers are most popular?
SELECT legs, COUNT(*) as ticket_count, 
       AVG(stake_amount), AVG(bonus_amount)
FROM settled_tickets 
WHERE bonus_applied = true
GROUP BY legs
ORDER BY legs;
6. A/B test plan (701% Parlay Bonus)
Create a comprehensive A/B test plan to measure retention impact:

Test Structure:

text
Control: No bonus
Promo Group A: Standard tiered bonus (2%-701%)
Promo Group B: Accelerated tiers (5%-1500% but lower max payout)
Target Metrics:

Primary: D1 deposits +25%

Secondary: Parlay volume increase, first-time parlay users

Retention: D1/D7/D30 active users

Guardrails: Bonus cost per user, average wager size

Test Parameters:

Sample size calculation

Duration (min 2 full weeks)

Segmentation (by deposit value, parlay history)

Exclusion rules (whales, bonus abusers)

Success criteria:

text
D1 deposits: +25% vs control ✓
Parlay volume: +15% vs control ✓
Bonus cost/user: <€25 ✓
7. SQL tracking queries for A/B test
Production SQL for test monitoring:

Daily deposit tracking:

sql
-- D1 deposits by test group
SELECT test_group, 
       COUNT(DISTINCT player_id) as unique_depositors,
       SUM(deposit_amount) as total_deposits
FROM deposits d
JOIN ab_test_groups t ON d.player_id = t.player_id
WHERE d.deposit_date = CURRENT_DATE - 1
  AND t.test_name = 'PARLAY701'
GROUP BY test_group;
Parlay volume by tier:

sql
-- Parlay engagement by bonus tier
SELECT t.test_group, 
       tt.legs,
       COUNT(*) as parlay_count,
       AVG(tt.stake_amount) as avg_stake
FROM tickets tt
JOIN ab_test_groups t ON tt.player_id = t.player_id
WHERE tt.ticket_type = 'PARLAY'
  AND tt.settlement_date >= CURRENT_DATE - 7
GROUP BY t.test_group, tt.legs;
8. Localized promo materials (Serbia)
Create a production-ready email template for Serbian market:

Subject lines (A/B test):

"701% BONUS na akumulator! 🏆"

"DO 701% VIŠE na tvoj akumulator!"

"Akumulator bonus: 701% za 40+ parova!"

Email body structure:

text
[Header: AdmiralBet logo + 701% badge]

🎯 NAJBOLJI AKUMULATOR BONUS U SRBIJI!

Napuni akumulator sa 40+ parova i OSVOJI DO 701% BONUSA!

📊 Tabela bonusa:
3 para = 2% bonus
...
40+ parova = 701% bonus! 🔥

✅ MINIMALNI KOTEFS: 1.30 po paru
✅ MAKS. ISPLATA: 21.000.000 RSD
✅ WAGERING: 5x na keš tiketima

[Bonus calculator widget]
[CTA: "NAPRAVI AKUMULATOR SADA" -> /sportsbook]

Pogodi više, osvoji više! ⚽️🏀🎾
Include:

responsive HTML structure

Serbian market terminology

legal disclaimers (responsible gaming)

UTM tracking parameters

9. Implementation risks + mitigations
List key risks:

Bonus abuse (arbitrage, bonus hunting)

Technical calculation errors

Payout cap bypass attempts

Wagering requirement confusion

A/B test contamination

10. Rollout recommendation
Phase 1: Soft launch (10% traffic, existing players)

Phase 2: A/B test (4 weeks)

Phase 3: Full rollout + email campaign

Phase 4: Optimization based on results

Output rules
Write like a Product Owner handing off to dev, marketing, and trading teams

Use exact numbers from context (701%, 21M RSD, x5 wagering, 1.30 min odds)

Make SQL queries production-ready and realistic

Reflect Serbian market context (RSD, local terminology)

Position as "I led from concept to implementation"

Use tables for bonus tiers and A/B results

Include realistic edge cases and error conditions

Technical realism layer:

Assume bonus must calculate in real-time during bet builder

Assume parlay legs can void mid-process affecting tier

Assume players can have multiple concurrent promos

Assume SQL must handle high-volume (10k+ tickets/hour)

Assume email deliverability requires double-opt-in compliance
