# Homegrid – Home Energy Simulator

Browser-based simulator of a home's electricity use, supplied by solar, battery storage, a diesel generator and the grid. No build step or dependencies: open the HTML file.

## Apps

### `index.html` – Live dashboard

A running clock (pause, 1x to 1800x, jump to any time, step between days) with an animated power-flow diagram. Flip a switch and demand changes immediately.

- **Distribution board.** Everything enters the house through a main breaker and a DB board with 7 circuits (lights & misc, HVAC, oven, hot water, laundry, kitchen sockets, EV charger). Each breaker shows live amps against its rating, and you choose the ratings. A circuit that stays overloaded trips (faster the bigger the overload); sustained demand above the main breaker's rating trips the main. Click a breaker to switch it off or reset it.
- **Diesel generator (5 kW).** Off / Run / Auto. Auto starts on an outage when the battery falls to 20% and charges it to 80%. Tracks tank level (20 L), fuel burn (idle 0.35 L/h + 0.27 L/kWh), diesel price and a wear-and-service cost per hour, and shows running cost per hour, cost per kWh, today's total and the cost at full load.
- **Expandable battery pack.** Add or remove 5 kWh modules (up to 12, i.e. 60 kWh). Each module adds 2.5 kW of power capability, capped by the inverter. A newly added module is empty, so state of charge drops until it fills.
- **Weather and temperature.** The daily curve is asymmetric (lowest near sunrise, warmest around 15:00, slower cooling at night), with day-to-day variation, small fluctuations, and a narrower swing under cloud. Indoor temperature follows a simple thermal model (insulation, sun through windows, internal heat) so the HVAC works against a real load, and switching it off lets the house warm up.
- **Schedules.** Per appliance, any number of entries: time, on/off, days of the week, plus run time (cycle appliances) or kWh target (EV). Example: hot water on at 04:00 daily, washing machine Mon/Wed/Sat only, a longer oven roast on Sundays. Schedules are saved in the browser.
- **Solar and cloud.** Arrays up to 30 kWp. Output falls linearly with cloud cover (100% cloud leaves 15% as diffuse light). Set a fixed cloud % or switch on dynamic weather, where the slider becomes the average and cloud fronts drift through the day. The panel shows the live cloud % and the resulting array output.
- **Grid control.** "Cut grid connection" opens the main isolator (or click the main breaker in the diagram) so the house runs only on solar, battery and generator. "Grid outage" simulates a utility cut. An "Export to grid" switch turns export off, so surplus solar is curtailed once the battery is full.
- **Also:** peak/off-peak/feed-in tariffs, a live timeline of the day, and a running daily bill (grid + fuel + wear - export).

### `planner.html` – Day planner

Static 24-hour planner: set each appliance's schedule and see the day's energy balance, cost, self-sufficiency and battery cycles.

## Model notes

- 230 V single phase; currents are kW / 230.
- Solar: bell-shaped output by season and sky condition, 85% system efficiency.
- Battery: 95% one-way efficiency, reserve level, self-consumption or off-peak grid charging.
- Dispatch order: solar, then generator, then battery, then grid.
