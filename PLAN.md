# PLAN (written before the code)

## Goal
CLI tool that generates, runs, and repairs pytest tests for one Python module and reports
coverage before/after.

## Architecture
- `autotest/cli.py`: command-line entry point.
- `autotest/agent.py`: agent loop (read code, generate tests, run, read errors, repair, max 3 rounds).
- `autotest/tools.py`: `read_file`, `run_pytest`, `get_coverage` (the tools the LLM may call).
- `autotest/report.py`: prints/saves the before/after report.
- `benchmark/evaluate.py`: runs the benchmark and computes coverage and mutation score.
- Generated tests run only in a sandboxed `workdir/` folder.

## MVP (by Mon 16 Nov)
Works end to end on 2 small repos; coverage increases on both; results saved in `results/`.

## Milestones
| Date | Goal |
|---|---|
| by 11 Nov | Proposal submitted |
| by 16 Nov | Checkpoint: MVP works end to end, PLAN.md, AGENTS.md, first agent log |
| 17 Nov - 29 Nov | Coverage-guided retry, error handling, benchmark repos, mutation testing |
| 30 Nov - 5 Dec | Full evaluation, README, REFLECTION.md, backup video |
| Sun 6 Dec | Code freeze: tag v1.0 |

## Evaluation plan
5-8 small open-source repos. Compare (a) one-shot LLM, (b) agent loop, (c) agent loop with
coverage-guided retry. Metrics: coverage before/after, pass rate, mutation score. 3 runs each.

## Who does what
| Member | Part |
|---|---|
| [Member 1] | Agent loop and tools |
| [Member 2] | CLI and reporting |
| [Member 3] | Benchmark, evaluation harness, tests |

## Risks
- LLM rate limits / cost: cache LLM results; strong model for planning, cheaper for routine edits.
- Non-deterministic output: repeat runs 3 times and average.
- Unsafe generated code: run only in `workdir/`.
