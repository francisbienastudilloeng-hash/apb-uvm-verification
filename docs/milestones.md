# Milestones

Roadmap for the APB4 slave register file + UVM testbench project.

## Roadmap

| Milestone | What | Analogy / output |
|---|---|---|
| **M0** | Spec + verification plan | The sign on the wall (what we're building) |
| **M1** | RTL | The locker cabinet |
| **M2** | Interface + top | The wires connecting everything |
| **M3** | "Hello UVM" | The empty skeleton runs |
| **M4** | Sequence item | The to-do note |
| **M5** | Driver | Hands |
| **M6** | Monitor | Eyes |
| **M7** | Agent + env | Group them into a team |
| **M8** | Scoreboard | The judge |
| **M9** | Coverage | The checklist |
| **M10** | Tests | Game plans (normal, random, error cases) |
| **M11** | Virtual sequences | Orchestrate reset → config → traffic |
| **M12** | SVA | Tripwires |
| **M13** | RAL | The labelled map |
| **M14** | Closure | Prove you're done: all tests pass, coverage reaches 100% |

### M0 breakdown

| Part | What it is | Output file |
|---|---|---|
| **M0a: Spec / register map** | Decide what the DUT does: registers, addresses, access types, reset values, error behaviour, wait states | `docs/register_map.md` |
| **M0b: Verification plan** | For each feature in the spec, decide how to prove it works: a test, a coverage point or an assertion | `docs/verification_plan.md` |

M0 lessons:

1. What a register map is: offsets, access types (RW/RO/WO/W1C), reset values
2. Illegal accesses: unmapped/misaligned addresses, writing RO registers, `PSLVERR`
3. The APB4 extras: `PSTRB`, `PPROT`, `PREADY` wait states
4. Design your own map (4–8 registers)
5. Verification plan: turning each row into tests, coverage and assertions

## UVM components: who does what

| Piece | Job | Analogy |
|---|---|---|
| **Sequence / sequence item** | Describes a transaction ("WRITE 0xFF to 0x04") | A to-do note |
| **Sequencer** | Hands those notes out one by one | A manager |
| **Driver** | Turns a note into real pin wiggles on APB | Hands |
| **Monitor** | Watches the pins and turns them back into notes | Eyes (it never touches anything) |
| **Scoreboard + reference model** | Checks whether the DUT's answer was right | A judge with an answer key |
| **Coverage** | Records which scenarios have happened | A checklist |
| **Assertions (SVA)** | Rules checked every clock cycle, e.g. "PENABLE never rises without PSEL" | Tripwires |
| **RAL** (register abstraction layer) | A software-style model of the register map: `regs.CTRL.write(5)` | A labelled map of the lockers |
| **Agent / env / test** | Containers that group the pieces and pick the scenario | Teams and a game plan |
