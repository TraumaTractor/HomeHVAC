# Homegrid – Home Energy Simulator

Browser-based simulator of a home's electricity use, supplied by solar, battery storage and the grid. No build step or dependencies: open the HTML file.

## Apps

- **`index.html` – Live dashboard.** A running clock (pause, 1x to 1800x), animated power-flow diagram, and appliance switches (HVAC with thermostat, hot water, washing machine, dryer, oven, microwave, kettle, EV charger, plus a misc load slider). Flip a switch and demand changes immediately. Includes an autopilot daily routine, grid-outage mode, battery modes, tariffs and a running daily bill.
- **`planner.html` – Day planner.** Static 24-hour planner: set each appliance's schedule and see the whole day's energy balance, cost, self-sufficiency and battery cycles.

## Model

- 5-minute (planner) or continuous (live) simulation steps
- Solar: bell-shaped output by season and sky condition, 85% system efficiency
- Battery: 95% one-way efficiency, reserve level, self-consumption or off-peak grid charging
- Grid: import and export limits, peak/off-peak/feed-in pricing, outage (islanded) mode
