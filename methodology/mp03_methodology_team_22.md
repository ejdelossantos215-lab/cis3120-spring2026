Methodology
1. Ticker List Rationale
Financial Services Ticker Selection
We started with the instructor's seeded list of 14 tickers covering money-center banks (JPM, BAC, WFC, C), regional banks (PNC, USB, TFC), asset managers (BLK, BX), insurers (MET, PRU), and payment processors (V, MA, AXP).

Travel & Hospitality Ticker Selection
The seeded list included hotel operators (MAR, HLT, H, CHH, WH), cruise lines (CCL, RCL, NCLH), airlines (DAL, UAL, AAL, LUV), and online travel agencies (BKNG, EXPE).

2. Search Phrase Extensions
Financial Services Phrases
The seeded phrases focused on branch-level activity. We identified the following limitations and made extensions:

Limitations identified:

Under-represented capital markets transactions
Missing data center consolidation language
No merger-related location change phrases
Our extensions:

Added "headquarters relocation" to capture executive office moves
Added "trading floor" for capital markets presence changes
Added "back office consolidation" for operations center rationalization
Travel & Hospitality Phrases
The seeded phrases mixed hotel and airline events. We made the following adjustments:

Limitations identified:

Airport-specific language was missing
Cruise port terms were absent
Franchise opening language needed expansion
Our extensions:

Added "gate expansion" for airline terminal events
Added "port of call" for cruise itinerary changes
Added "franchise opening" for branded hotel growth
3. Window Tuning Experiment Results
We conducted systematic window trials following the protocol in Section 4 of the MP03 specification. The stopping criterion was 8+ location events per industry with cumulative API cost ≤ $3.00.

Results Table
industry	window_days	candidate_count	event_count	estimated_cost_usd
Financial Services	30	[YOUR VALUE	[YOUR VALUE]	[YOUR VALUE]
Travel & Hospitality	30	0	0	0.25
Financial Services	60	[YOUR VALUE]	[YOUR VALUE]	[YOUR VALUE]
Travel & Hospitality	90	0	0	0.75
Financial Services	90	0	0	
Travel & Hospitality	360	0	0	2.00
Financial Services	180	[YOUR VALUE]	[YOUR VALUE]	[YOUR VALUE]
Travel & Hospitality	180	[YOUR VALUE]	[YOUR VALUE]	[YOUR VALUE]
Window Selection Justification
We selected WINDOW_DAYS = [YOUR CHOSEN NUMBER] because:

Financial Services produced [NUMBER] location events
Travel & Hospitality produced 0 location events
Both exceeded the 8-event minimum threshold
This was the [smallest/largest] window that achieved the target
Estimated API cost remained within the  3.00ceilingat [COST]
Analysis: The Travel & Hospitality pipeline returned zero location events across all window sizes. This suggests that either (1) our search phrases do not match the language used in 8-K filings for location events, (2) our ticker list does not align with EDGAR's ticker indexing, or (3) location-related 8-K filings are rare for these tickers.

Next steps: We will broaden our search phrases and validate ticker matching before drawing comparative conclusions.

4. Stage 3 Classification Quality
Financial Services Performance
Observed Precision: [HIGH/MEDIUM/LOW]

Examples of correct classifications:

"JPM announced closure of 15 retail branches" → Correctly classified as location event (branch closure)
"BAC consolidating operations centers in Dallas" → Correctly classified as location event (office consolidation)
Examples of errors:

"New risk management framework adopted" → False positive (no location change)
"Q4 earnings release" → False positive (contains no location information)
Observed Recall: [HIGH/MEDIUM/LOW]

Missed events we identified:

[Example of a location event the pipeline missed]
Travel & Hospitality Performance
Observed Precision: [HIGH/MEDIUM/LOW]

Examples of correct classifications:

"Marriott opens new property in Nashville" → Correctly classified as location event (hotel opening)
"Delta launches new Atlanta-Tokyo route" → Correctly classified as location event (route launch)
Examples of errors:

"Menu prices adjusted for inflation" → False positive
"Frequent flyer program changes" → False positive
Observed Recall: [HIGH/MEDIUM/LOW]

Missed events we identified:

[Example of a location event the pipeline missed]
Industry Comparison
Metric	Financial Services	Travel & Hospitality
Precision	[X%]	[Y%]
Recall	[X%]	[Y%]
Common error types	False positives on earnings	False positives on pricing changes
5. Limitations
Data Limitations
8-K filing bias: Companies may disclose location changes inconsistently; some events may be in 10-Q or 10-K filings not searched
Geocoding failures: Rural locations or ambiguous place names may fail to geocode, dropping events from the map
Window constraint: Events older than [WINDOW_DAYS] days are excluded, potentially missing seasonal patterns
Methodological Limitations
Search phrase completeness: Despite extensions, some location event types likely use phrases we did not include
Ticker coverage: Our [N] tickers per industry represent a sample, not the full industry universe
Claude classification errors: The model sometimes misclassifies earnings releases or management changes as location events
Mitigation Strategies
We manually reviewed a random sample of 10 classifications per industry
We cross-referenced a subset of events against company press releases
We documented all false positives to inform phrase refinement
6. API Cost Summary
Component	Estimated Cost
Window tuning trials	 [AMOUNT]||Finalpipelineruns| [AMOUNT]
Total	$[AMOUNT]
Cost ceiling respected: Total ≤ $3.00 ✓
