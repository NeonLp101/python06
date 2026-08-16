# python06

42 Heilbronn — Python module 06: the import system.

How Python finds, loads and namespaces modules — demonstrated by a small
`alchemy` package that is deliberately built to expose the edge cases.

## Layout

```
alchemy/
├── __init__.py         re-exports a subset, aliases healing_potion as heal
├── elements.py         create_earth, create_air
├── potions.py          imports from BOTH .elements and top-level elements
├── grimoire/           light_spellbook + validator, and a circular dark pair
└── transmutation/      recipes.py, re-exported through __init__
elements.py             top-level module — same name as alchemy/elements.py
```

`alchemy/potions.py` imports from `.elements` and from `elements` in the same
file, which is what makes the shadowing visible: the leading dot decides which
of the two modules you get.

## Exercises

| Script | Demonstrates |
|---|---|
| `ft_alembic_0` | `import elements` — top-level module |
| `ft_alembic_1` | `from elements import ...` |
| `ft_alembic_2` | `import alchemy.elements` — the package submodule |
| `ft_alembic_3` | `from alchemy.elements import ...` |
| `ft_alembic_4` | `import alchemy` — reaches `create_air`, but `create_earth` was never re-exported, so it raises |
| `ft_alembic_5` | `from alchemy import ...` |
| `ft_distillation_0` | Direct access to `alchemy.potions` |
| `ft_distillation_1` | The same functions through the package, including the `heal` alias |
| `ft_kaboom_0` | The light spellbook, which imports cleanly |
| `ft_kaboom_1` | The dark spellbook — `dark_spellbook` and `dark_validator` import each other, so this raises |
| `ft_transmutation_0` | `import alchemy.transmutation.recipes as recipes` |
| `ft_transmutation_1` | `import alchemy.transmutation` — resolved via the subpackage `__init__` |
| `ft_transmutation_2` | `import alchemy` — resolved via two levels of re-export |

`ft_alembic_4` and `ft_kaboom_1` are meant to fail. That is the exercise.

## Running

```
python3 ft_alembic_0.py
```
