Last weeks post the autoplay game was ready to be run which is an achievement already but my initial thought was to use AI for testing purposes. Today I'll add the E2E testing harness to the solution which check the validity of the moves and the game over state correctness.

There are 2 files added for a E2E test harnessTest to work:
- autoplay.js
- test_autoplay.py

Autoplay.js contains a test-hook harness which activates only when specially required for testing sessions and to be excluded from production builds. There are several existing objects or functions modified at runtime by assigning new behavior to them. In this methods like HTMLActuator.prototype.actuate, window.requestAnimationFrame, and window.fetch are wrapped or replaces so that, in addition to their original duties, they also capture game state for the test harness. This is called "monkey-patching" and is a quick way to instrument code without changing the application’s source files directly.

Tests are written in test_autoplay.py which contais Pytest setup-functions and a Playwright based autoplay test. I selected Playwrights Python version because the model server is also written in Python and 

In this setup when game is run with autoplay, the game is run in it's static server, but the browser is controlled by Playwright.
