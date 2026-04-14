Prompt:
You are a senior iGaming Product Designer + Product Manager + Sportsbook UX strategist with experience in multi-market betting products.
Use the following real project context and produce a structured product specification for Player Props homepage highlights at AdmiralBet.

Context
I worked at AdmiralBet as Product Owner / Head of Trading and optimized the UX for player props, especially bets like LeBron total points. Originally, these props were visible mainly on the match page. I redesigned the experience so that the most relevant player props could also be surfaced on the homepage as dynamic highlights, while still linking back to the full match and market details. This approach increased visibility and improved play rate by approximately 20%. I also worked with developers so that internal users could choose what to highlight by day, week, or month, depending on business priorities and current sports trends.

AdmiralBet operates across multiple markets, including:

Serbia
Croatia
Montenegro
Bosnia & Herzegovina
Nigeria
Uganda

For this exercise, assume the following commercial logic:
Serbia = higher margin market
Nigeria = lower margin market

The other markets should sit between those two extremes, with sensible configuration differences based on localization, commercial strategy, and UX simplicity
Also assume player props require near real-time odds updates, and industry APIs commonly expose player prop data by event, market type, player label, line, and over/under odds.

Your task
Create a complete product specification for a dynamic homepage highlight module for Player Props.
Deliverables
Provide the output in the exact structure below:

1. Product goal
Write a short problem statement, user need, business need, and expected impact.

2. Figma wireframe spec
Create a text-based Figma-ready wireframe spec for:

Homepage dynamic highlight module

Match page entry point

Expanded player props card

Internal admin/control logic for choosing highlights

For each screen/component include:

Frame name

Purpose

Layout structure

UI components

States

Interaction notes

Mobile and desktop behavior

The highlight module must support:

User choice or admin choice of daily / weekly top props

Prop example: LeBron James – Total Points

CTA to open full market or full match page

Odds refresh behavior

Highlight tags such as “Trending”, “Top Played”, “Boosted”, “Ending Soon”

3. API specification
Define realistic example API calls and response payloads for:

Fetch highlighted props

Fetch odds for a highlighted prop

Fetch market metadata by country/market

Record click, betslip add, and placement events for analytics

Use REST-style examples with:

endpoint

method

params

sample request

sample JSON response

Include fields such as:

eventId

marketId

playerId

playerName

statType

line

overOdds

underOdds

marginProfile

country

displayPriority

highlightWindow (daily/weekly)

tags

lastUpdated

isSuspended

4. Metrics section
Use the following project result as an input assumption:

Homepage surfacing of player props increased play rate by 20%

Build a metrics framework with:

Primary KPI

Secondary KPIs

Guardrail metrics

Funnel stages

Then provide:

Baseline vs expected uplift table

Formula for play rate

Formula for CTR to prop details

Formula for betslip conversion

Clear explanation of how this 20% boost should be measured in production

5. Multi-market config JSON
Generate a single JSON config example for AdmiralBet player props across 6 markets:

Serbia

Croatia

Montenegro

Bosnia & Herzegovina

Nigeria

Uganda

The JSON must include for each market:

countryCode

currency

marginTier

targetMarginPercent

oddsFormat

decimalPlaces

highlightEnabled

defaultHighlightWindow

topTagsEnabled

boostedOddsEnabled

maxHomepageCards

lowLatencyOddsRefreshSeconds

showPlayerImage

showTrendBadge

showMarketCount

localization notes

Commercial assumptions:

Serbia = high margin

Nigeria = low margin

Others = medium variations between them

6. Margin and odds display strategy
Explain how UX and pricing display should differ between:

High-margin markets like Serbia

Low-margin markets like Nigeria

Cover:

Odds visibility

Refresh cadence

badge usage

promotional emphasis

simplicity vs density of information

trust and clarity considerations

7. A/B test plan
Create a detailed A/B test plan to improve retention and repeat engagement through player props highlights.

Include:

Hypothesis

Control

Variant A

Variant B

Target segments

Success metrics

Guardrails

Test duration

Sample event taxonomy

Decision criteria

Use iGaming A/B testing best practices such as:

running tests for at least a full weekly cycle

prioritizing hypotheses around engagement drop-off and retention

using segmented test groups rather than random generic changes only

The experiment should focus on:

whether dynamic homepage highlights improve retention vs match-page-only discovery

whether daily vs weekly curation performs better

whether “Trending / Top Played” labels improve repeat usage

8. Risks and mitigations
List the main product, operational, trading, and technical risks with mitigation actions.

9. Final recommendation
Give a concise recommendation for rollout order across markets.

Output rules
Be specific, practical, and product-oriented

Write like a senior product manager preparing a handoff for design, engineering, analytics, and trading teams

Use tables where useful

Use clean JSON blocks

Avoid generic theory

Keep all examples relevant to sportsbook player props and AdmiralBet context

Kako da ga koristiš bolje
Ako želiš odgovor koji je još više “tvoj”, dodaj na kraj prompta i ovaj deo:

Add this personalization layer:

Position the solution as if it was led by a Product Owner with strong trading understanding

Emphasize cooperation with developers and internal trading/content teams

Reflect real sportsbook constraints: margin protection, odds suspension, event start timing, and market prioritization

Keep examples centered on basketball player props, but make the framework reusable for other sports
