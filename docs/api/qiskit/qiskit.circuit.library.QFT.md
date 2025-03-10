---
title: QFT
description: API reference for qiskit.circuit.library.QFT
in_page_toc_min_heading_level: 1
python_api_type: class
python_api_name: qiskit.circuit.library.QFT
---

# QFT

<span id="qiskit.circuit.library.QFT" />

`qiskit.circuit.library.QFT(num_qubits=None, approximation_degree=0, do_swaps=True, inverse=False, insert_barriers=False, name=None)`

Bases: `BlueprintCircuit`

Quantum Fourier Transform Circuit.

The Quantum Fourier Transform (QFT) on $n$ qubits is the operation

$$
|j\rangle \mapsto \frac{1}{2^{n/2}} \sum_{k=0}^{2^n - 1} e^{2\pi ijk / 2^n} |k\rangle
$$

The circuit that implements this transformation can be implemented using Hadamard gates on each qubit, a series of controlled-U1 (or Z, depending on the phase) gates and a layer of Swap gates. The layer of Swap gates can in principle be dropped if the QFT appears at the end of the circuit, since then the re-ordering can be done classically. They can be turned off using the `do_swaps` attribute.

For 4 qubits, the circuit that implements this transformation is:

![../\_images/qiskit-circuit-library-QFT-1.png](/images/api/qiskit/qiskit-circuit-library-QFT-1.png)

The inverse QFT can be obtained by calling the `inverse` method on this class. The respective circuit diagram is:

![../\_images/qiskit-circuit-library-QFT-2.png](/images/api/qiskit/qiskit-circuit-library-QFT-2.png)

One method to reduce circuit depth is to implement the QFT approximately by ignoring controlled-phase rotations where the angle is beneath a threshold. This is discussed in more detail in [https://arxiv.org/abs/quant-ph/9601018](https://arxiv.org/abs/quant-ph/9601018) or [https://arxiv.org/abs/quant-ph/0403071](https://arxiv.org/abs/quant-ph/0403071).

Here, this can be adjusted using the `approximation_degree` attribute: the smallest `approximation_degree` rotation angles are dropped from the QFT. For instance, a QFT on 5 qubits with approximation degree 2 yields (the barriers are dropped in this example):

![../\_images/qiskit-circuit-library-QFT-3.png](/images/api/qiskit/qiskit-circuit-library-QFT-3.png)

Construct a new QFT circuit.

**Parameters**

*   **num\_qubits** ([*int*](https://docs.python.org/3/library/functions.html#int "(in Python v3.12)") *| None*) – The number of qubits on which the QFT acts.
*   **approximation\_degree** ([*int*](https://docs.python.org/3/library/functions.html#int "(in Python v3.12)")) – The degree of approximation (0 for no approximation).
*   **do\_swaps** ([*bool*](https://docs.python.org/3/library/functions.html#bool "(in Python v3.12)")) – Whether to include the final swaps in the QFT.
*   **inverse** ([*bool*](https://docs.python.org/3/library/functions.html#bool "(in Python v3.12)")) – If True, the inverse Fourier transform is constructed.
*   **insert\_barriers** ([*bool*](https://docs.python.org/3/library/functions.html#bool "(in Python v3.12)")) – If True, barriers are inserted as visualization improvement.
*   **name** ([*str*](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)") *| None*) – The name of the circuit.

## Attributes

<span id="qiskit.circuit.library.QFT.ancillas" />

### ancillas

Returns a list of ancilla bits in the order that the registers were added.

<span id="qiskit.circuit.library.QFT.approximation_degree" />

### approximation\_degree

The approximation degree of the QFT.

**Returns**

The currently set approximation degree.

<span id="qiskit.circuit.library.QFT.calibrations" />

### calibrations

Return calibration dictionary.

The custom pulse definition of a given gate is of the form `{'gate_name': {(qubits, params): schedule}}`

<span id="qiskit.circuit.library.QFT.clbits" />

### clbits

Returns a list of classical bits in the order that the registers were added.

<span id="qiskit.circuit.library.QFT.data" />

### data

<span id="qiskit.circuit.library.QFT.do_swaps" />

### do\_swaps

Whether the final swaps of the QFT are applied or not.

**Returns**

True, if the final swaps are applied, False if not.

<span id="qiskit.circuit.library.QFT.extension_lib" />

### extension\_lib

`= 'include "qelib1.inc";'`

<span id="qiskit.circuit.library.QFT.global_phase" />

### global\_phase

Return the global phase of the circuit in radians.

<span id="qiskit.circuit.library.QFT.header" />

### header

`= 'OPENQASM 2.0;'`

<span id="qiskit.circuit.library.QFT.insert_barriers" />

### insert\_barriers

Whether barriers are inserted for better visualization or not.

**Returns**

True, if barriers are inserted, False if not.

<span id="qiskit.circuit.library.QFT.instances" />

### instances

`= 264`

<span id="qiskit.circuit.library.QFT.layout" />

### layout

Return any associated layout information about the circuit

This attribute contains an optional [`TranspileLayout`](qiskit.transpiler.TranspileLayout "qiskit.transpiler.TranspileLayout") object. This is typically set on the output from [`transpile()`](compiler#qiskit.compiler.transpile "qiskit.compiler.transpile") or [`PassManager.run()`](qiskit.transpiler.PassManager#run "qiskit.transpiler.PassManager.run") to retain information about the permutations caused on the input circuit by transpilation.

There are two types of permutations caused by the [`transpile()`](compiler#qiskit.compiler.transpile "qiskit.compiler.transpile") function, an initial layout which permutes the qubits based on the selected physical qubits on the [`Target`](qiskit.transpiler.Target "qiskit.transpiler.Target"), and a final layout which is an output permutation caused by [`SwapGate`](qiskit.circuit.library.SwapGate "qiskit.circuit.library.SwapGate")s inserted during routing.

<span id="qiskit.circuit.library.QFT.metadata" />

### metadata

The user provided metadata associated with the circuit.

The metadata for the circuit is a user provided `dict` of metadata for the circuit. It will not be used to influence the execution or operation of the circuit, but it is expected to be passed between all transforms of the circuit (ie transpilation) and that providers will associate any circuit metadata with the results it returns from execution of that circuit.

<span id="qiskit.circuit.library.QFT.num_ancillas" />

### num\_ancillas

Return the number of ancilla qubits.

<span id="qiskit.circuit.library.QFT.num_clbits" />

### num\_clbits

Return number of classical bits.

<span id="qiskit.circuit.library.QFT.num_parameters" />

### num\_parameters

<span id="qiskit.circuit.library.QFT.num_qubits" />

### num\_qubits

The number of qubits in the QFT circuit.

**Returns**

The number of qubits in the circuit.

<span id="qiskit.circuit.library.QFT.op_start_times" />

### op\_start\_times

Return a list of operation start times.

This attribute is enabled once one of scheduling analysis passes runs on the quantum circuit.

**Returns**

List of integers representing instruction start times. The index corresponds to the index of instruction in `QuantumCircuit.data`.

**Raises**

[**AttributeError**](https://docs.python.org/3/library/exceptions.html#AttributeError "(in Python v3.12)") – When circuit is not scheduled.

<span id="qiskit.circuit.library.QFT.parameters" />

### parameters

<span id="qiskit.circuit.library.QFT.prefix" />

### prefix

`= 'circuit'`

<span id="qiskit.circuit.library.QFT.qregs" />

### qregs

`list[QuantumRegister]`

A list of the quantum registers associated with the circuit.

<span id="qiskit.circuit.library.QFT.qubits" />

### qubits

Returns a list of quantum bits in the order that the registers were added.

## Methods

### inverse

<span id="qiskit.circuit.library.QFT.inverse" />

`inverse()`

Invert this circuit.

**Returns**

The inverted circuit.

**Return type**

[*QFT*](#qiskit.circuit.library.QFT "qiskit.circuit.library.basis_change.qft.QFT")

### is\_inverse

<span id="qiskit.circuit.library.QFT.is_inverse" />

`is_inverse()`

Whether the inverse Fourier transform is implemented.

**Returns**

True, if the inverse Fourier transform is implemented, False otherwise.

**Return type**

[bool](https://docs.python.org/3/library/functions.html#bool "(in Python v3.12)")

