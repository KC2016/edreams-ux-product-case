# eDreams Product Case Study: E-Commerce Funnel & UX Analysis
**Executive Summary**

This case study evaluates the end-to-end user experience (UX) and product design of the eDreams mobile and desktop e-commerce booking funnel. The analysis was conducted through a real-time purchasing simulation, navigating from the initial flight search up to the final checkout screen.

To demonstrate a structured, iterative product methodology, this repository is organized into a multi-stage roadmap:

**Stage 1 (Completed):** User Experience (UX) & Accessibility Audit.

**Stage 2 (Completed):** Data-Driven Metric Mapping & Cart Abandonment Deep Dive.

**Stage 3 (Future Roadmap):** Dynamic Pricing & Ancillary Revenue Optimization.

## Stage 1: UX & Accessibility Audit (Current Project)
### 1. Friction Points & Areas for Improvement
#### A. Geolocation-Locked Language & Currency Inflexibility

🔴 **High Friction**

The Issue: While the platform allows users to select their preferred country market (storefront), it creates an inflexible, forced bundle between the selected country, its official language, and its local currency. For instance, if a user manually selects Spain as their market, the system automatically forces the interface into Spanish and the currency into Euros, without offering an independent setting to change the display language back to English or any other preferred language.

UX Impact: This creates a severe barrier for expatriates and digital nomads who reside in a country but do not speak the local language. By strictly pairing the storefront market with a single language, the platform forces non-native speakers to navigate complex booking and legal terms in a foreign language or rely on inaccurate browser translations, disrupting an otherwise smooth checkout funnel.

#### B. Dynamic Font Layout Break (Accessibility Bug)

🟠 **UI / Accessibility Bug**

The Issue: On the baggage selection screen, an important promotional banner highlighted in orange ("Maletas hasta un -20% más...") suffered severe text truncation. The crucial parts of the text were completely hidden underneath the selection block.

UX Impact: The interface fails to support dynamic/responsive system fonts (a setting heavily used by visually impaired users who increase text size on their operating systems). Because the text collapsed, the layout overlapped, rendering the promotional messaging unreadable.

<img src="images/font.jpeg" alt="Dynamic Font Accessibility Bug" width="300">

#### C. Inconsistent "Desglose del Precio" (Price Breakdown) Behavior

🟠 **UX Inconsistency**

The Issue: The price breakdown tool works flawlessly and transparently across most stages of the funnel. However, it completely breaks on the specific screen offering refundable tickets. Clicking "Desglose" on this screen fails to isolate the cost of the insurance and only displays the consolidated total price.

UX Impact: Technical inconsistency at a critical touchpoint. Hiding the exact financial breakdown during a high-value cross-selling stage triggers user defense mechanisms, making customers reject the service out of fear of hidden fees.

<img src="images/desglose.jpeg" alt="Price Breakdown Bug Screen" width="300">

#### D. Static and Linear Seat Pricing

🟢 **Revenue Opportunity**

The Issue: The seat selection screen charges the exact same fee for middle, window, or aisle seats within the same cabin zone.

UX Impact: Middle seats are universally perceived as the worst flight experience. A flat rate fails to respect user preferences or leverage the higher perceived value of windows and aisles.

#### E. Weak Address and Postal Code Validation

🔵 **Operational Risk**

The Issue: During the simulation, the system accepted a completely mismatched address combination (City: Barcelona / Postal Code: 53442), even though Barcelona postal codes strictly begin with "08".

UX Impact: A lack of real-time address verification API integration at this stage creates data hygiene issues and risks billing failures.

### 2. Conversions Drivers (What eDreams Does Well)
Despite the friction points, the platform demonstrates several strong product design choices:

Clean and Fluid UI: The overall interface is visually pleasing, leveraging a non-invasive color palette that guides the user effortlessly without causing cognitive fatigue.

Balanced Cross-Selling: Although the funnel actively offers add-ons like extra baggage, travel insurance, seat selection, and refundable ticket upgrades, these cross-selling modules do not derail the user's main purchase intent.

Route Flexibility: The system smoothly allows users to buy independent legs of a journey (e.g., departure with one airline, return with another), maximizing customer choice.

Efficient Scarcity Triggers: Displaying the exact number of low remaining seats on a flight serves as an excellent psychological trigger to accelerate the final decision.

Value-Added Features: The option to "Freeze Price" is a brilliant product feature that directly mitigates user anxiety surrounding volatile airline tariffs.

### Future Roadmap: Suggestions for Upcoming Studies
To expand this case study into an end-to-end Product Management portfolio, the following phases are mapped out for future iterations:

## Stage 2: Data-Driven Metric Mapping & Cart Abandonment Deep Dive

### 📌 Objective & Hypothesis
We translated the qualitative UX friction points from Stage 1 into core e-commerce metrics using tracking logs generated in `01_data_generation.ipynb` to test the following premise:
* **Hypothesis:** The lack of transparency in the "Prime Price" coupled with the language-locking mechanism is the primary cause of a high independent Drop-Off Rate at the cart/checkout level for international cohorts.

### 📈 Metrics Implementation & Regional Drill-Down
Instead of looking at a generic global abandonment rate, metrics were calculated independently per market segment to prevent high-volume core hubs (like Spain) from masking localized conversion drops:

$$\text{Market Abandonment Rate} = \frac{\text{Total Abandoned Checkout Sessions within Market } X}{\text{Total Checkout Sessions within Market } X} \times 100$$

* Data processing inside the notebook successfully cross-tabulated `user_market` and user `status` to isolate the exact impact of language restriction on conversion.

### 🧪 A/B Testing Experiment Design
To validate a potential solution (implementing a decentralized "Language/Currency Select" toggle at checkout), we built a mathematical framework to size the experiment under strict statistical guardrails:

* **Baseline Conversion Rate:** 4.0% (Derived from our historical production funnel log baseline).
* **Minimum Detectable Effect (MDE):** 15% relative lift (Targeting a **4.6%** conversion rate for the variant group).
* **Statistical Thresholds:** Alpha ($\alpha$) = 0.05 (95% Confidence Level) | Statistical Power ($1-\beta$) = 0.80.

#### Sample Size Framework Results
Using `statsmodels.stats.power`, the mandatory sample thresholds calculated to achieve statistical significance are:
* **Required Sample Size PER VARIANT:** 17,923 unique sessions
* **Total Minimum Traffic Required:** 35,846 unique sessions

---

## 💰 Future Roadmap: Stage 3 (Dynamic Pricing & Ancillary Revenue Optimization)
Objective: Optimize financial revenue models without hurting the core user experience.

* **Focus Area 1 (Pricing Algorithms):** Revamping the seat map into a dynamic pricing structure (charging a premium for window/aisle demand and introducing discounts to offload middle seats faster).
* **Focus Area 2 (Accessibility & Upselling Conversion):** Resolving the dynamic font bug identified in Stage 1 to calculate the potential recovery of Ancillary Revenue (baggage upsells) among visually impaired user demographics.
* **Focus Area 3 (Risk Mitigation):** Integrating international postal APIs (like Loqate or Google Places) to analyze the decrease in payment-stage transaction declines.

---

### 🎯 Conclusion
This multi-stage roadmap demonstrates the evolution of a product mindset: beginning with an empathetic User UX Audit (Stage 1), transitioning into Data-Driven Metrics (Stage 2), and culminating in Business & Revenue Optimization (Stage 3).

## References:
### Methodology & Industry Benchmarks
The synthetic dataset used in this analysis mimics real-world production data for the travel sector, adhering to industry performance data provided by:
- **Conversion Rates (~4%):** Validated against *Contentsquare's Digital Experience Benchmarks*.
- **Funnel Drop-offs (~75%):** Modeled after *SaleCycle's Airline & Travel Abandonment Reports* (accounting for price comparison behaviors and ancillary fee friction).
- **Technical Failures (~3%):** Based on industry-standard web platform SLA error budgets (*Datadog/SRE principles*).


