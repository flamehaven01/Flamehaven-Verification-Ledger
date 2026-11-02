# NSRW core scalars: fifteen checks through a second arithmetic path

## Result

Five scalar enclosures at each of 128, 256 and 512 fractional bits passed full
interval containment checks. The checked quantities are normalized endpoints
ell and v, plateau width, weight gap and the main-coefficient denominator.

The producer uses exact Fraction arithmetic, positive series and bounded
remainders. The checker uses mpmath 1.3.0 interval arithmetic with direct
exponential differences. It imports no producer code.

| Fractional bits | Working bits | Containment checks |
| --- | --- | --- |
| 128 | 320 | 5/5 PASS |
| 256 | 448 | 5/5 PASS |
| 512 | 704 | 5/5 PASS |

## Why it matters

The positive scalar factors are computational building blocks for the proved
NSRW angular-margin result. A second arithmetic implementation can detect
algorithm-specific interval errors that deterministic producer replay alone
would repeat. The exact mathematics, numerical inputs and computation are now
connected to one inspectable execution record.

## Reproduce and inspect

- [Exact checker](https://github.com/flamehaven01/NavierStokes-Research-Workbench/blob/bd5da25381f59034bc9d0f2506a82d255790b30b/scripts/check-core-scalars-mpmath.py)
- [Checker tests](https://github.com/flamehaven01/NavierStokes-Research-Workbench/blob/bd5da25381f59034bc9d0f2506a82d255790b30b/tests/test_core_scalar_crosscheck.py)
- [Method and command](https://github.com/flamehaven01/NavierStokes-Research-Workbench/blob/bd5da25381f59034bc9d0f2506a82d255790b30b/docs/NSRW_CORE_SCALAR_CROSSCHECK.md)
- [Retained result](https://github.com/flamehaven01/NavierStokes-Research-Workbench/blob/bd5da25381f59034bc9d0f2506a82d255790b30b/examples/p2-core-scalars/mpmath-crosscheck.json)
- [Math-to-code architecture](https://github.com/flamehaven01/NavierStokes-Research-Workbench/blob/bd5da25381f59034bc9d0f2506a82d255790b30b/docs/NSRW_MATH_TO_CODE_BRIDGE.md)
- [Research website](https://flamehaven01.github.io/NavierStokes-Research-Workbench/)
- [Research writing](https://flamehaven.space/writing/from-a-scale-invariant-candidate-to-an-obstruction-what-changed-while-reproducing-a-navierstokes-construction/)

The optional verification dependency is mpmath==1.3.0. Execute the checker with
the three retained JSON files as inputs. The method page supplies the complete
command and explains the tested operations of mpmath's interval context.

## Identity and interpretation

NSRW implementation checkpoint: `bd5da25381f59034bc9d0f2506a82d255790b30b`.
Local retained result SHA-256 (LF bytes): `4d1b584f5ca89db5f3779808523d225c60b7c50f7c3d3df0d5df9825c0f98f4f`.
Each record includes both its executor's raw input digest and an LF-normalized
portable input digest. Line-ending normalization is not a numeric change.

The algorithm and backend differ; the operator is shared. This record checks
core scalar intervals. Source model admissibility, coefficients and a complete
numerical J certificate are the next research work. It neither reruns Lean nor
changes the existing named-proposition receipts.

## Architecture ownership

NSRW owns the executable checker and the single architecture map. This EQA
entry and its API expose the observed cross-check result. Both sites remain
usable without a runtime dependency on the other site's API.

## Reading the arithmetic analysis

A containment PASS means that the entire checker interval lies inside the
producer's retained rational endpoints. It is stronger than matching midpoints.
The input record's fractional precision b specifies an absolute dyadic grid;
the second checker operates at b + 192 working bits.

The two arithmetic paths use different expression forms. The Fraction producer
uses factored expm1 with a direct positive series. The mpmath checker evaluates
the original exponential differences for G and D, as well as the normalized
endpoints and plateau width. At lambda = 10^-12 the support gap is about
3.84e-18; its small size motivates explicit error control, not a claim of
binary64 underflow.

The local J margin involves K1, c1, I01 and the support weight gap. These scalar
checks evaluate the gap and a conservative normalized moment factor. Affine
coefficient bounds and admissible model inputs are the next calculation needed
to turn those factors into a numerical J certificate.
