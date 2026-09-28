# Easy to use Scientific Calculator

A single-file scientific calculator that runs in any modern browser. It works with a very wide range of numbers: results can be anywhere from **10⁻⁹⁹⁹⁹ to 10⁹⁹⁹⁹**, with exact decimal arithmetic.

## Quick start

1. Open `scientific-calculator.html` in a browser (double-click it).
2. Start typing with the on-screen keys or your keyboard.

There is nothing to install and no internet connection is needed. The only dependency, [decimal.js](https://github.com/MikeMcl/decimal.js) v10.6.0 (MIT licence), is embedded in the file.

## Features

- **Big range:** answers from 10⁻⁹⁹⁹⁹ to 10⁹⁹⁹⁹, shown in scientific notation when very large or very small (e.g. `1×10⁹⁹⁹⁹`).
- **Exact decimal maths:** `0.1 + 0.2` gives exactly `0.3`. Calculations use 64 digits internally and show 12 significant digits.
- **Live result:** the answer appears under your expression as you type. Press `=` to commit it.
- **Natural display:** stacked fractions, raised exponents and a proper root symbol, all editable in place.
- **Functions:** `sin`, `cos`, `tan`, `ln`, `log` (base 10), `√` with any index, `π` and `e`.
- **DEG / RAD toggle** in the top-right corner for trig functions.

## Keys

| Key | What it does |
| --- | --- |
| `AC` | Clear everything |
| `←` `→` | Move the cursor |
| `⌫` | Delete (removes a whole function name like `sin(` in one press) |
| `a⁄b` | Stacked fraction. If a number is just before the cursor, it becomes the numerator |
| `x²` `x³` `xⁿ` | Insert an exponent. `xⁿ` leaves the exponent empty for you to fill in |
| `√` | Root template `root(2, ...)`. Click the small index to change it (3 for cube root, etc.) |
| `sin` `cos` `tan` `ln` `log` | Insert the function with an opening bracket |
| `π` `e` | Constants |
| `=` | Evaluate and put the answer back in the editor |

Click an exponent, root index, numerator or denominator on screen to move the cursor into it.

### Keyboard shortcuts

| Key | Action |
| --- | --- |
| `0`–`9` `.` `+` `-` `*` `/` `(` `)` | Type as normal |
| `^` | Insert an exponent |
| `e` / `p` | Insert e / π |
| `Enter` or `=` | Evaluate |
| `Backspace` | Delete |
| `Esc` | Clear |
| `←` `→` | Move the cursor |

## Examples

| To calculate | Press |
| --- | --- |
| e² = 7.38905609893 | `e` `xⁿ` `2` |
| 10⁹⁹⁹⁹ = 1×10⁹⁹⁹⁹ | `1` `0` `xⁿ` `9` `9` `9` `9` |
| 10⁻⁹⁹⁹⁹ = 1×10⁻⁹⁹⁹⁹ | `1` `0` `xⁿ` `−` `9` `9` `9` `9` |
| sin 30° = 0.5 | `sin` `3` `0` (in DEG mode) |
| 2π = 6.28318530718 | `2` `π` |
| ∛27 = 3 | `√`, click the index, change it to `3`, then enter `27` in the body |

## Number range and errors

- **Displayed results** must lie between about 10⁻⁹⁹⁹⁹ and 10⁹⁹⁹⁹. Outside that, the result line shows **Out of range (too large)** or **Out of range (too small)**.
- **Intermediate steps** may go much further, so `(10^10000) ÷ (10^10000)` still works and gives 1.
- Numbers of 10¹² or more, and non-zero numbers below 10⁻⁹, are shown in scientific notation. Everything else is shown in plain form.
- Invalid input (such as `1÷0`, `ln(0)`, `tan(90°)`, or an even root of a negative number) shows nothing while typing and **Error** after `=`.

To change the range, edit `MAX_EXP` near the top of the script section (default `9999`).

## How expressions are evaluated

- Normal precedence: powers, then `×` `÷`, then `+` `−`. Unary minus binds looser than powers, so `−5²` is `−25`.
- **Implicit multiplication** works: `2π`, `3(4+1)`, `2sin(30)`.
- **Chained exponents** are applied left to right, matching how they look on screen: `3` `x²` `x³` is (3²)³ = 729.
- After `=`, pressing an exponent key applies the power to the whole answer, even if it is negative or in scientific notation.
- A missing closing bracket at the end of an expression is filled in automatically.
- In DEG mode, angles are reduced exactly, so `sin(180)` is exactly `0` and `cos(90)` is exactly `0`.

## Known limitations

- After `=`, typing more digits adds them to the answer. Press `AC` to start fresh.
- Pressing `a⁄b` after a large scientific answer shows the fraction as plain text rather than stacked.
- The answer is rounded to 12 significant digits when it is placed back in the editor, so chained calculations carry that rounding.
- 0⁰ is treated as 1.
