# A Practical Guide to Python Data Structures for Hospital Management

[![Releases](https://img.shields.io/badge/releases-python_data_structures-blue?logo=github&logoColor=white)](https://github.com/JeevanJundale/Python_Data_Structures/releases)

🏥🐍 A practical guide to Python data structures for hospital management systems. This repo shows how common structures map to real-world tasks in a hospital. All code targets Python 3.13 and uses zero external dependencies. It stresses clear thinking, reliable behavior, and readable code.

---

## Table of contents

- [About this project](#about-this-project)
- [Key ideas](#key-ideas)
- [How it maps to hospital workflows](#how-it-maps-to-hospital-workflows)
- [Getting started](#getting-started)
- [Run the demo locally](#run-the-demo-locally)
- [Code examples](#code-examples)
- [Data structures in depth](#data-structures-in-depth)
- [API reference](#api-reference)
- [Testing and validation](#testing-and-validation)
- [Design notes and best practices](#design-notes-and-best-practices)
- [Project structure](#project-structure)
- [Contributing](#contributing)
- [Licenses and attribution](#licenses-and-attribution)
- [Where to find assets](#where-to-find-assets)

---

## About this project

This repository is a comprehensive guide to Python data structures presented through hospital management analogies. It aims to demystify core concepts by showing how everyday hospital tasks align with standard data structures. The narrative uses realistic pain points—patient flow, inventory checks, staff authentication, and sterile tool management—to illustrate how Python containers behave, how memory patterns work, and how to write robust, readable code.

Key points:
- Python 3.13 is the target platform.
- All examples run with zero external dependencies.
- The focus is hands-on learning, not theoretical abstraction.
- The material doubles as a lightweight reference for practical coding in a hospital setting.

---

## Key ideas

- Data structures are tools for organizing, storing, and accessing information.
- Real-world processes in a hospital can be modeled with these tools to improve clarity and reliability.
- Clear interfaces and small, well-scoped examples reduce bugs and improve maintainability.
- Tests and demos help verify that the structures behave as expected in typical workflows.

---

## How it maps to hospital workflows

- Patient admission uses a queue-like structure to manage who gets care next, with priority handling for urgent cases.
- Emergency room (ER) processing relies on a fast, flexible queue to pull the next patient for assessment.
- Medication dispensing uses a stack-like approach when handling recent orders or stacked inventory in a controlled sequence.
- Doctor login demonstrates password handling and verification, mirroring secure access control.
- Equipment sterilization reflects set-like operations to track contamination and clearance.

These mappings help learners see why a particular data structure is suitable for a given problem. They also encourage thinking in terms of invariants, performance expectations, and edge cases.

---

## Getting started

Before you begin, ensure you have Python 3.13 installed. The examples assume a standard, single-machine setup and use built-in libraries only.

- Install Python 3.13 from the official source if you have not already.
- Clone the repository to your local machine using the standard workflow.
- Prepare to run the demo script that demonstrates the hospital workflow end-to-end.

Note on assets: The latest release assets contain a demo runner file. Download the file hospital_system.py from the release asset bundle and run it to see the workflow in action. You can access the releases here: https://github.com/JeevanJundale/Python_Data_Structures/releases. For convenience, the same link is repeated here: https://github.com/JeevanJundale/Python_Data_Structures/releases.

---

## Run the demo locally

To reproduce the demo on your machine, follow these steps:

1) Clone the repository
- Use the official remote to clone the project:
  - git clone https://github.com/JeevanJundale/Python_Data_Structures.git
  - cd Python_Data_Structures

2) Download and run the demo script
- From the releases page, download the demo asset that includes hospital_system.py.
- Extract the asset if needed.
- Run the demo:
  - python hospital_system.py

3) Optional test credentials
- The demo includes a sample user:
  - Username: dr_grey
  - Password: SeattleGrace1!  (pre-registered in the demo)

4) Explore the code
- Open student-friendly modules under src/ or examples/ (paths may vary by release).
- Read the inline comments to see the one-to-one mappings to hospital tasks.

If you prefer to skip setup, you can explore the live, prebuilt examples in the released assets and run the included runner file.

---

## Code examples

The core ideas are shown with compact, readable Python 3.13 code. Each snippet maps to a hospital workflow.

Admitting a patient with priority:
```python
def admit_patient(name: str, reason: str, priority: bool = False) -> dict:
    """Add a patient to the intake queue with optional priority."""
    patient = {"name": name, "reason": reason, "priority": priority}
    if priority:
        # insert at the front for urgent cases
        patient_queue.appendleft(patient)
    else:
        patient_queue.append(patient)
    return patient
```

ER processing example:
```python
from collections import deque

er_queue = deque()

# add patients
er_queue.append({"name": "Alice", "condition": "Chest Pain"})
er_queue.append({"name": "Bob", "condition": "Fracture"})

# get next patient for assessment
next_patient = er_queue.popleft()
```

Medication dispensing using a stack:
```python
med_stack = []

# store meds
med_stack.append("Aspirin 100mg")
med_stack.append("Morphine 2mg")

# dispense last prescribed medication
dispensed = med_stack.pop()
```

Doctor login verification:
```python
import hashlib, os

def hash_password(password: str, salt: bytes) -> str:
    return hashlib.pbkdf2_hmac("sha256", password.encode(), salt, 100000).hex()

def verify_password(stored_hash: str, salt: bytes, attempt: str) -> bool:
    return hash_password(attempt, salt) == stored_hash
```

Sterilization tracking with sets:
```python
sterile_tools = {"scalpel", "forceps", "gloves", "gowns"}
contaminated_tools = {"scalpel"}

# remove contaminated tools from sterile set
sterile_tools -= contaminated_tools
```

These snippets illustrate how to express common hospital actions with simple Python data structures. They also show how to keep data clean and operations predictable.

---

## Data structures in depth

Here is a deeper look at how each core structure maps to hospital tasks, with practical notes.

- Lists
  - Use cases: daily logs, ordered records, patient lists where order matters.
  - Pros: simple, fast for append and iteration.
  - Cons: insertions in the middle can be slow.

- Tuples
  - Use cases: fixed records like a patient snapshot that should not change.
  - Pros: lightweight and immutable, safe for defaults.
  - Cons: not suitable for mutable records.

- Dictionaries
  - Use cases: fast lookups by key, such as patient IDs to records.
  - Pros: O(1) average lookup, flexible schemas.
  - Cons: requires careful key management to avoid collisions.

- Sets
  - Use cases: track unique resources, such as unique equipment IDs.
  - Pros: fast membership tests, no duplicates.
  - Cons: unordered.

- Stacks and queues
  - Stacks: LIFO behavior, useful for last-in-first-out workflows in limited contexts.
  - Queues: FIFO behavior, perfect for patient intake and task dispatching.
  - Deques: double-ended queues that support append and pop from both ends, ideal for flexible front-end priority handling.

- Heaps (priority queues)
  - Use cases: prioritize urgent cases, or rank resource requests by priority or estimated wait times.
  - Pros: efficient retrieval of the highest-priority item.
  - Cons: slightly more complex to implement and reason about.

- Graphs (advanced)
  - Use cases: model patient transfer routes, staff scheduling networks, or dependency graphs for care plans.
  - Pros: captures complex relationships.
  - Cons: more challenging to implement and visualize.

- Memory considerations
  - Understand how Python stores references.
  - Prefer clear data models to reduce unexpected aliasing.
  - Use type hints to improve readability and maintenance.

- Testing mindset
  - Write tests that reflect hospital policies and edge cases.
  - Test for empty queues, full stacks, and invalid inputs.
  - Validate invariants, such as correct sequencing and no duplicate IDs where not allowed.

This depth helps you see not just how to use a structure, but how to reason about performance and correctness in a real system.

---

## API reference

Note: The API shown here is illustrative and aligned with the examples in the repository. Real implementations in the project may expose small variations or helper utilities.

- admit_patient(name: str, reason: str, priority: bool = False) -> dict
  - Adds a patient to the intake queue with an optional priority flag.
  - Returns a dictionary representing the patient record.

- next_patient() -> dict | None
  - Retrieves the next patient for care from the ER queue.
  - Returns a patient record or None if the queue is empty.

- add_medication(medication: str) -> None
  - Pushes a medication onto the dispensing stack.

- dispense_medication() -> str | None
  - Pops the most recently added medication from the stack.
  - Returns the medication name or None if empty.

- verify_password(stored_hash: str, salt: bytes, attempt: str) -> bool
  - Verifies a user-supplied password against a stored hash.
  - Returns True if the password matches.

- sterilize_tools(contaminated: set[str], sterile: set[str]) -> set[str]
  - Removes contaminated tools from the sterile set.
  - Returns the updated set.

- get_inventory() -> dict
  - Returns a dictionary mapping tool IDs to their status.

These APIs are designed to be approachable. They focus on clear intent and predictable behavior, which matters when you use them to teach or build simple hospital management demos.

---

## Testing and validation

- Unit tests cover common workflows, including:
  - Admit patients with and without priority and verification of queue order.
  - ER processing order and handling of empty queues.
  - Medication dispensing boundaries when the stack is empty.
  - Password verification with correct and incorrect attempts.
  - Sterilization logic removing contaminated items from the sterile set.

- Property tests confirm invariants, such as:
  - No duplicate patient IDs in a given view.
  - Priority patients appear before non-priority ones when appropriate.
  - Inventory updates reflect changes after adds and removals.

- End-to-end tests simulate a short sequence of hospital tasks to ensure the demo runner behaves as expected.

If you want to contribute tests, look for the tests/ directory in the repository copy you pull from releases. The tests follow the same style as the examples: small, readable, and domain-focused.

---

## Design notes and best practices

- Clarity over cleverness. The code aims to be easy to read and reason about.
- Small, focused functions with explicit inputs and outputs. Each function does one thing well.
- Type hints are used to communicate intent and help with tooling.
- Safe defaults. Functions treat missing data gracefully or raise clear errors.
- Documentation is inline wherever possible. Read the code and the accompanying comments to understand the rationale.
- Simple error handling. Don’t over-design; catch common misuses early and provide actionable messages.

---

## Project structure

- README.md
- hospital_system.py (demo runner in the release)
- src/
  - core.py (basic data structure wrappers and helpers)
  - workflows.py (mapping of hospital processes to data structures)
  - tests/
- docs/
  - concepts.md (detailed explanations)
  - best_practices.md

Note: The exact layout can vary by release. The demo asset for the releases page includes the primary runner file hospital_system.py as described above.

---

## Contributing

- Start from a clear problem statement. Show a hospital-anchored example.
- Write tests that reflect real-world use cases and edge cases.
- Keep changes small and incremental.
- Document behavior that might surprise readers, especially around edge cases like empty queues or empty stacks.
- Use the same naming style as the repository to keep the code cohesive.
- Follow Python style guidelines in PEP 8, with a focus on readability.

If you want to propose a new lesson or new data structure mapping, open an issue describing the scenario and provide a minimal, runnable example. Community contributions are welcome.

---

## Licenses and attribution

This guide uses Python 3.13 and standard library components. It does not introduce external dependencies. The examples are for educational purposes and aim to be clear and accurate. If you reuse any of the code in your own projects, credit the original author of this guide.

---

## Where to find assets

- Main releases page: https://github.com/JeevanJundale/Python_Data_Structures/releases
- Re-visit the same URL for the latest demo assets, example scripts, and downloadable walkthroughs. For convenience, the link is repeated here: https://github.com/JeevanJundale/Python_Data_Structures/releases

- To directly view the repository content, clone from the official repo:
  - git clone https://github.com/JeevanJundale/Python_Data_Structures.git

- The assets typically include a hospital_system.py script plus supplementary modules, sample data, and small utilities that illustrate the hospital-focused data structures in action. The demo runner hospital_system.py ties together the core concepts and shows how the pieces work in concert.

---

## Visuals and badges

- A bright badge at the top links to the releases and signals that you can grab ready-made demos and assets.
- Emojis are used to keep the tone approachable and add a quick visual cue for domain relevance.
- When you add new sections or release notes, consider adding a small badge that points to the relevant release or version.

---

## How to learn more

- Read each section with the mindset of translating a real hospital task into Python data structures.
- Re-implement the examples in your own words to reinforce understanding.
- Extend the demos by adding more complex scenarios, such as multi-priority queues with tie-breaking rules or inventory replenishment simulations.

---

## Quick start checklist

- [ ] Install Python 3.13
- [ ] Clone the repository
- [ ] Download hospital_system.py from the latest releases and run it
- [ ] Explore the core examples in the code base
- [ ] Try extending workflows with your own data

This guide is designed for learners who want a practical, readable path into Python data structures. It emphasizes real-world relevance, clear code, and maintainable practices. The hospital management lens helps keep concepts concrete and memorable.

---

## Final notes

This document is designed to be scanned quickly yet offer depth for readers who want to dive in. It keeps a steady focus on readability, practical demonstrations, and safe, straightforward code patterns. The hospital domain is used as a scaffold to teach core Python data structures in a way that stays accessible, not overwhelming.