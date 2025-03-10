---
title: PadDelay
description: API reference for qiskit_ibm_provider.transpiler.passes.scheduling.PadDelay
in_page_toc_min_heading_level: 1
python_api_type: class
python_api_name: qiskit_ibm_provider.transpiler.passes.scheduling.PadDelay
---

# PadDelay

<span id="qiskit_ibm_provider.transpiler.passes.scheduling.PadDelay" />

`PadDelay(fill_very_end=True, schedule_idle_qubits=False)`

Padding idle time with Delay instructions.

Consecutive delays will be merged in the output of this pass.

The ASAP-scheduled circuit output may become

```python
     ┌────────────────┐
q_0: ┤ Delay(160[dt]) ├──■──
     └─────┬───┬──────┘┌─┴─┐
q_1: ──────┤ X ├───────┤ X ├
           └───┘       └───┘
```

Note that the additional idle time of 60dt on the `q_0` wire coming from the duration difference between `Delay` of 100dt (`q_0`) and `XGate` of 160 dt (`q_1`) is absorbed in the delay instruction on the `q_0` wire, i.e. in total 160 dt.

See [`BlockBasePadder`](qiskit_ibm_provider.transpiler.passes.scheduling.BlockBasePadder "qiskit_ibm_provider.transpiler.passes.scheduling.BlockBasePadder") pass for details.

Create new padding delay pass.

**Parameters**

*   **fill\_very\_end** (`bool`) – Set `True` to fill the end of circuit with delay.
*   **schedule\_idle\_qubits** (`bool`) – Set to true if you’d like a delay inserted on idle qubits. This is useful for timeline visualizations, but may cause issues for execution on large backends.

## Attributes

<span id="paddelay-is-analysis-pass" />

### is\_analysis\_pass

Check if the pass is an analysis pass.

If the pass is an AnalysisPass, that means that the pass can analyze the DAG and write the results of that analysis in the property set. Modifications on the DAG are not allowed by this kind of pass.

<span id="paddelay-is-transformation-pass" />

### is\_transformation\_pass

Check if the pass is a transformation pass.

If the pass is a TransformationPass, that means that the pass can manipulate the DAG, but cannot modify the property set (but it can be read).

## Methods

<span id="paddelay-call" />

### \_\_call\_\_

<span id="qiskit_ibm_provider.transpiler.passes.scheduling.PadDelay.__call__" />

`PadDelay.__call__(circuit, property_set=None)`

Runs the pass on circuit.

**Parameters**

*   **circuit** (*QuantumCircuit*) – the dag on which the pass is run.
*   **property\_set** (*PropertySet or dict or None*) – input/output property set. An analysis pass might change the property set in-place.

**Returns**

**If on transformation pass, the resulting QuantumCircuit. If analysis**

pass, the input circuit.

**Return type**

QuantumCircuit

<span id="paddelay-name" />

### name

<span id="qiskit_ibm_provider.transpiler.passes.scheduling.PadDelay.name" />

`PadDelay.name()`

Return the name of the pass.

<span id="paddelay-run" />

### run

<span id="qiskit_ibm_provider.transpiler.passes.scheduling.PadDelay.run" />

`PadDelay.run(dag)`

Run the padding pass on `dag`.

**Parameters**

**dag** ([`DAGCircuit`](/api/qiskit/qiskit.dagcircuit.DAGCircuit.html#qiskit.dagcircuit.DAGCircuit "(in Qiskit v0.44)")) – DAG to be checked.

**Returns**

DAG with idle time filled with instructions.

**Return type**

DAGCircuit

**Raises**

**TranspilerError** – When a particular node is not scheduled, likely some transform pass is inserted before this node is called.

