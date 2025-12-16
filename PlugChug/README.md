## What this is

**Plug n Chugger** is a TI-BASIC utility that brute-forces values of **x**, **(x,y)**, or **(x,y,z)** over user-specified ranges and step sizes, and checks whether two user-entered expressions satisfy a chosen relation:

* `=`, `≠`, `<`, `≤`, `>`, `≥`

It records the variable values that pass the test into lists, and prints summary stats (counts and sums).

---

## How it works (high level)

1. On startup it **zeros accumulators** (`P,Q,H,T`) and clears Lists `L₃–L₆`
2. Shows a **main menu**:

   * **About**: displays instructions
   * **X**: scan a 1-variable range
   * **X,Y**: scan a 2-variable grid
   * **X,Y,Z**: scan a 3-variable grid
   * **QUIT**: stop program
3. For the chosen dimension, it shows a **relation menu** (`=`, `≠`, `<`, `≤`, `>`, `≥`, plus “INCR SOLVER”)
4. You enter:

   * step/jump size(s)
   * start/end bound(s)
   * two expressions as strings (parsed into `Y₁` and `Y₂`)
5. The program loops through the range(s), evaluates `Y₁` and `Y₂`, and if the relation is true:

   * increments **P** (number of solutions found)
   * accumulates sums (**Q** for x, **H** for y, **T** for z)
   * stores passing points into lists

---

## Outputs / where results are stored

Depending on mode:

### 1-variable mode (X)

* Passing x values → `L₃`
* Summary shown:

  * `P` = number of x’s that worked
  * `Q` = sum of those x’s

### 2-variable mode (X,Y)

* Passing x values → `L₃`
* Passing y values → `L₄`
* Summary shown:

  * `P` = number of (x,y) pairs that worked
  * `Q` = sum of x’s
  * `H` = sum of y’s

### 3-variable mode (X,Y,Z)

* Passing x values → `L₃`
* Passing y values → `L₄`
* Passing z values → `L₅`
* Summary shown:

  * `P` = number of (x,y,z) triples that worked
  * `Q` = sum of x’s
  * `H` = sum of y’s
  * `T` = sum of z’s

---

## Increment Solver (solving for `K`)

Instead of checking a relation directly, **Increment Solver** loops over x (and optionally y, z) and uses TI’s `solve(` to find a value `K` that makes:

[
Y₁ = Y₂
]

You provide:

* a guess `J`
* a search range `[N, O]` for `K`

Results saved as:

* `K` values → `L₃`
* corresponding x values → `L₄`
* (and y → `L₅`, z → `L₆` in higher-dim modes)

It also prints sums like `Σ of K’s = sum(L₃)` and sums of scanned variables.

By John Schmidt