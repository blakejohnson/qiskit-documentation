---
title: DynamicCircuitInstructionDurations
description: API reference for qiskit_ibm_provider.transpiler.passes.scheduling.DynamicCircuitInstructionDurations
in_page_toc_min_heading_level: 1
python_api_type: class
python_api_name: qiskit_ibm_provider.transpiler.passes.scheduling.DynamicCircuitInstructionDurations
---

# DynamicCircuitInstructionDurations

<span id="qiskit_ibm_provider.transpiler.passes.scheduling.DynamicCircuitInstructionDurations" />

`DynamicCircuitInstructionDurations(instruction_durations=None, dt=None, enable_patching=True)`

For dynamic circuits the IBM Qiskit backend currently reports instruction durations that differ compared with those required for the legacy Qobj-based path. For now we use this class to report updated InstructionDurations. TODO: This would be mitigated by a specialized Backend/Target for dynamic circuit backends.

Dynamic circuit instruction durations.

## Attributes

<span id="dynamiccircuitinstructiondurations-measure-patch-cycles" />

### MEASURE\_PATCH\_CYCLES

<span id="qiskit_ibm_provider.transpiler.passes.scheduling.DynamicCircuitInstructionDurations.MEASURE_PATCH_CYCLES" />

`= 160`

<span id="dynamiccircuitinstructiondurations-measure-patch-odd-offset" />

### MEASURE\_PATCH\_ODD\_OFFSET

<span id="qiskit_ibm_provider.transpiler.passes.scheduling.DynamicCircuitInstructionDurations.MEASURE_PATCH_ODD_OFFSET" />

`= 64`

## Methods

<span id="dynamiccircuitinstructiondurations-from-backend" />

### from\_backend

<span id="qiskit_ibm_provider.transpiler.passes.scheduling.DynamicCircuitInstructionDurations.from_backend" />

`classmethod DynamicCircuitInstructionDurations.from_backend(backend)`

Construct an `InstructionDurations` object from the backend.

**Parameters**

**backend** ([`Backend`](/api/qiskit/qiskit.providers.Backend.html#qiskit.providers.Backend "(in Qiskit v0.44)")) – backend from which durations (gate lengths) and dt are extracted.

**Returns**

The InstructionDurations constructed from backend.

**Return type**

InstructionDurations

**Raises**

**TranspilerError** – If dt and dtm is different in the backend.

<span id="dynamiccircuitinstructiondurations-get" />

### get

<span id="qiskit_ibm_provider.transpiler.passes.scheduling.DynamicCircuitInstructionDurations.get" />

`DynamicCircuitInstructionDurations.get(inst, qubits, unit='dt', parameters=None)`

Get the duration of the instruction with the name, qubits, and parameters.

Some instructions may have a parameter dependent duration.

<Admonition title="Deprecated since version 0.19.0" type="danger">
  Using a Qubit or List\[Qubit] for the `qubits` argument to InstructionDurations.get() is deprecated as of qiskit-terra 0.19.0. It will be removed no earlier than 3 months after the release date. Instead, use an integer for the qubit index.
</Admonition>

**Parameters**

*   **inst** (*str |* [*qiskit.circuit.Instruction*](/api/qiskit/qiskit.circuit.Instruction.html#qiskit.circuit.Instruction "(in Qiskit v0.44)")) – An instruction or its name to be queried.
*   **qubits** (*int | list\[int] | Qubit | list\[Qubit] | list\[int | Qubit]*) – Qubits or its indices that the instruction acts on.
*   **unit** (*str*) – The unit of duration to be returned. It must be ‘s’ or ‘dt’.
*   **parameters** (*list\[float] | None*) – The value of the parameters of the desired instruction.

**Returns**

The duration of the instruction on the qubits.

**Return type**

float|int

**Raises**

**TranspilerError** – No duration is defined for the instruction.

<span id="dynamiccircuitinstructiondurations-units-used" />

### units\_used

<span id="qiskit_ibm_provider.transpiler.passes.scheduling.DynamicCircuitInstructionDurations.units_used" />

`DynamicCircuitInstructionDurations.units_used()`

Get the set of all units used in this instruction durations.

**Return type**

`set`\[`str`]

**Returns**

Set of units used in this instruction durations.

<span id="dynamiccircuitinstructiondurations-update" />

### update

<span id="qiskit_ibm_provider.transpiler.passes.scheduling.DynamicCircuitInstructionDurations.update" />

`DynamicCircuitInstructionDurations.update(inst_durations, dt=None)`

Update self with inst\_durations (inst\_durations overwrite self). Overrides the default durations for certain hardcoded instructions.

**Parameters**

*   **inst\_durations** (`Union`\[`List`\[`Tuple`\[`str`, `Optional`\[`Iterable`\[`int`]], `float`, `Optional`\[`Iterable`\[`float`]], `str`]], `List`\[`Tuple`\[`str`, `Optional`\[`Iterable`\[`int`]], `float`, `Optional`\[`Iterable`\[`float`]]]], `List`\[`Tuple`\[`str`, `Optional`\[`Iterable`\[`int`]], `float`, `str`]], `List`\[`Tuple`\[`str`, `Optional`\[`Iterable`\[`int`]], `float`]], [`InstructionDurations`](/api/qiskit/qiskit.transpiler.InstructionDurations.html#qiskit.transpiler.InstructionDurations "(in Qiskit v0.44)"), `None`]) – Instruction durations to be merged into self (overwriting self).
*   **dt** (`Optional`\[`float`]) – Sampling duration in seconds of the target backend.

**Returns**

The updated InstructionDurations.

**Return type**

InstructionDurations

**Raises**

**TranspilerError** – If the format of instruction\_durations is invalid.

