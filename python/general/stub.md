# Python: Stubs

In Python, the term **"stub"** has three common meanings depending on the context. It can refer to type hint files, objects used in testing, or simple placeholder code.

---

### 1. Type Hint Stubs (`.pyi` files)

This is the most common and modern meaning. A stub file is a text file with a `.pyi` extension that acts as an "interface" or "header file" for a Python module. It contains all the function signatures, variable, and class definitions with type hints, but **no implementation**. The implementation is replaced with an ellipsis (`...`).

**Key Purpose:** To provide type information for static type checkers (like `mypy` or `Pyright`) when the actual source code (`.py`) doesn't have type hints.

**Common Use Cases:**
*   Adding types to a third-party library you can't modify.
*   Providing types for compiled C extension modules (e.g., NumPy).
*   Separating type definitions from the runtime code for clarity.

**Example:**

A simple, untyped module `math_utils.py`:
```python
# math_utils.py
def add(a, b):
    return a + b

PI = 3.14

# math_utils.pyi
# Note: Implementations are replaced with '...'
def add(a: int, b: int) -> int: ...

PI: float