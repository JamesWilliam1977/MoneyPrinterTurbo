```markdown
# MoneyPrinterTurbo Development Patterns

> Auto-generated skill from repository analysis

## Overview
This skill document outlines the key development patterns, coding conventions, and workflows used in the MoneyPrinterTurbo Python codebase. It is designed to help contributors quickly understand the repository's practices, from file naming and import styles to specialized refactoring workflows and testing patterns.

## Coding Conventions

### File Naming
- **CamelCase** is used for file names.
  - Example: `MoneyPrinterService.py`, `DataLoader.py`

### Import Style
- **Relative imports** are preferred within the package.
  - Example:
    ```python
    from .utils import calculate_interest
    from ..models import Transaction
    ```

### Export Style
- **Named exports** are used; functions and classes are explicitly defined for import.
  - Example:
    ```python
    def generate_report(...):
        ...

    class MoneyPrinter:
        ...
    ```

## Workflows

### Refactor Hardcoded Data to JSON
**Trigger:** When you want to move large hardcoded data structures (like lists or dicts) out of Python files for better maintainability.
**Command:** `/extract-data-to-json`

1. **Extract Data:** Create a new JSON file in the appropriate `app/services/data/` directory containing the extracted data.
    - Example: Move a hardcoded list from `MoneyPrinterService.py` to `app/services/data/interest_rates.json`.
2. **Update Code:** Modify the relevant Python service (`app/services/*.py`) to load the data from the new JSON file. Use a helper function or caching mechanism if needed.
    - Example:
      ```python
      import json
      from pathlib import Path

      def load_interest_rates():
          with open(Path(__file__).parent / 'data' / 'interest_rates.json') as f:
              return json.load(f)
      ```
3. **Add/Update Tests:** Add or update regression tests in `test/services/test_*.py` to ensure the refactor does not change behavior.
    - Example:
      ```python
      def test_interest_rate_loading():
          rates = load_interest_rates()
          assert rates['USD'] == 0.05
      ```

**Files Involved:**
- `app/services/data/*.json`
- `app/services/*.py`
- `test/services/test_*.py`

**Frequency:** ~2x/month

## Testing Patterns

- **Test File Pattern:** Test files are named with the pattern `*.test.*` (e.g., `MoneyPrinterService.test.py`).
- **Framework:** The specific testing framework is unknown, but standard Python testing practices apply.
- **Regression Testing:** After significant refactors (like data extraction), regression tests are added or updated to ensure no behavioral changes.

## Commands

| Command                | Purpose                                                               |
|------------------------|-----------------------------------------------------------------------|
| /extract-data-to-json  | Refactor hardcoded data from Python files into JSON with regression tests |
```
