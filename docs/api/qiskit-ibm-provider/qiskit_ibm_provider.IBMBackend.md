---
title: IBMBackend
description: API reference for qiskit_ibm_provider.IBMBackend
in_page_toc_min_heading_level: 1
python_api_type: class
python_api_name: qiskit_ibm_provider.IBMBackend
---

# IBMBackend

<span id="qiskit_ibm_provider.IBMBackend" />

`IBMBackend(configuration, provider, api_client, instance=None)`

Backend class interfacing with an IBM Quantum device.

You can run experiments on a backend using the [`run()`](qiskit_ibm_provider.IBMBackend#run "qiskit_ibm_provider.IBMBackend.run") method. The [`run()`](qiskit_ibm_provider.IBMBackend#run "qiskit_ibm_provider.IBMBackend.run") method takes one or more [`QuantumCircuit`](/api/qiskit/qiskit.circuit.QuantumCircuit.html#qiskit.circuit.QuantumCircuit "(in Qiskit v0.44)") and returns an `IBMJob` instance that represents the submitted job. Each job has a unique job ID, which can later be used to retrieve the job. An example of this flow:

```python
from qiskit import transpile
from qiskit_ibm_provider import IBMProvider
from qiskit.circuit.random import random_circuit

provider = IBMProvider()
backend = provider.backend.ibmq_vigo
qx = random_circuit(n_qubits=5, depth=4)
transpiled = transpile(qx, backend=backend)
job = backend.run(transpiled)
retrieved_job = provider.backend.retrieve_job(job.job_id())
```

<Admonition title="Note" type="note">
  *   Unlike `qiskit.execute()`, the [`run()`](qiskit_ibm_provider.IBMBackend#run "qiskit_ibm_provider.IBMBackend.run") method does not transpile the circuits for you, so be sure to do so before submitting them.
  *   You should not instantiate the `IBMBackend` class directly. Instead, use the methods provided by an [`IBMProvider`](qiskit_ibm_provider.IBMProvider "qiskit_ibm_provider.IBMProvider") instance to retrieve and handle backends.
</Admonition>

Other methods return information about the backend. For example, the [`status()`](qiskit_ibm_provider.IBMBackend#status "qiskit_ibm_provider.IBMBackend.status") method returns a [`BackendStatus`](/api/qiskit/qiskit.providers.models.BackendStatus.html#qiskit.providers.models.BackendStatus "(in Qiskit v0.44)") instance. The instance contains the `operational` and `pending_jobs` attributes, which state whether the backend is operational and also the number of jobs in the server queue for the backend, respectively:

```python
status = backend.status()
is_operational = status.operational
jobs_in_queue = status.pending_jobs
```

**Here is list of attributes available on the `IBMBackend` class:**

*   name: backend name.

*   backend\_version: backend version in the form X.Y.Z.

*   num\_qubits: number of qubits.

*   target: A [`qiskit.transpiler.Target`](/api/qiskit/qiskit.transpiler.Target.html#qiskit.transpiler.Target "(in Qiskit v0.44)") object for the backend.

*   basis\_gates: list of basis gates names on the backend.

*   gates: list of basis gates on the backend.

*   local: backend is local or remote.

*   simulator: backend is a simulator.

*   conditional: backend supports conditional operations.

*   open\_pulse: backend supports open pulse.

*   memory: backend supports memory.

*   max\_shots: maximum number of shots supported.

*   coupling\_map (list): The coupling map for the device

*   supported\_instructions (List\[str]): Instructions supported by the backend.

*   dynamic\_reprate\_enabled (bool): whether delay between programs can be set dynamically (ie via `rep_delay`). Defaults to False.

*   rep\_delay\_range (List\[float]): 2d list defining supported range of repetition delays for backend in μs. First entry is lower end of the range, second entry is higher end of the range. Optional, but will be specified when `dynamic_reprate_enabled=True`.

*   default\_rep\_delay (float): Value of `rep_delay` if not specified by user and `dynamic_reprate_enabled=True`.

*   n\_uchannels: Number of u-channels.

*   u\_channel\_lo: U-channel relationship on device los.

*   meas\_levels: Supported measurement levels.

*   qubit\_lo\_range: Qubit lo ranges for each qubit with form (min, max) in GHz.

*   meas\_lo\_range: Measurement lo ranges for each qubit with form (min, max) in GHz.

*   dt: Qubit drive channel timestep in nanoseconds.

*   dtm: Measurement drive channel timestep in nanoseconds.

*   rep\_times: Supported repetition times (program execution time) for backend in μs.

*   meas\_kernels: Supported measurement kernels.

*   discriminators: Supported discriminators.

*   hamiltonian: An optional dictionary with fields characterizing the system hamiltonian.

*   channel\_bandwidth (list): Bandwidth of all channels (qubit, measurement, and U)

*   acquisition\_latency (list): Array of dimension n\_qubits x n\_registers. Latency (in units of dt) to write a measurement result from qubit n into register slot m.

*   conditional\_latency (list): Array of dimension n\_channels \[d->u->m] x n\_registers. Latency (in units of dt) to do a conditional operation on channel n from register slot m

*   meas\_map (list): Grouping of measurement which are multiplexed

*   max\_circuits (int): The maximum number of experiments per job

*   sample\_name (str): Sample name for the backend

*   n\_registers (int): Number of register slots available for feedback (if conditional is True)

*   register\_map (list): An array of dimension n\_qubits X n\_registers that specifies whether a qubit can store a measurement in a certain register slot.

*   configurable (bool): True if the backend is configurable, if the backend is a simulator

*   credits\_required (bool): True if backend requires credits to run a job.

*   online\_date (datetime): The date that the device went online

*   display\_name (str): Alternate name field for the backend

*   description (str): A description for the backend

*   tags (list): A list of string tags to describe the backend

*   version: version of `Backend` class (Ex: 1, 2)

*   channels: An optional dictionary containing information of each channel – their purpose, type, and qubits operated on.

*   parametric\_pulses (list): A list of pulse shapes which are supported on the backend. For example: `['gaussian', 'constant']`

*   processor\_type (dict): Processor type for this backend. A dictionary of the form `{"family": <str>, "revision": <str>, segment: <str>}` such as `{"family": "Canary", "revision": "1.0", segment: "A"}`.

    > *   family: Processor family of this backend.
    > *   revision: Revision version of this processor.
    > *   segment: Segment this processor belongs to within a larger chip.

IBMBackend constructor.

**Parameters**

*   **configuration** (`Union`\[[`QasmBackendConfiguration`](/api/qiskit/qiskit.providers.models.QasmBackendConfiguration.html#qiskit.providers.models.QasmBackendConfiguration "(in Qiskit v0.44)"), [`PulseBackendConfiguration`](/api/qiskit/qiskit.providers.models.PulseBackendConfiguration.html#qiskit.providers.models.PulseBackendConfiguration "(in Qiskit v0.44)")]) – Backend configuration.
*   **provider** ([`IBMProvider`](qiskit_ibm_provider.IBMProvider "qiskit_ibm_provider.ibm_provider.IBMProvider")) – IBM Quantum account provider.
*   **api\_client** (`AccountClient`) – IBM Quantum client used to communicate with the server.

## Attributes

<span id="ibmbackend-coupling-map" />

### coupling\_map

Return the [`CouplingMap`](/api/qiskit/qiskit.transpiler.CouplingMap.html#qiskit.transpiler.CouplingMap "(in Qiskit v0.44)") object

<span id="ibmbackend-dt" />

### dt

<span id="qiskit_ibm_provider.IBMBackend.dt" />

`float | None`

Return the system time resolution of input signals

This is required to be implemented if the backend supports Pulse scheduling.

**Returns**

The input signal timestep in seconds. If the backend doesn’t define `dt` `None` will be returned

**Return type**

dt

<span id="ibmbackend-dtm" />

### dtm

<span id="qiskit_ibm_provider.IBMBackend.dtm" />

`float`

Return the system time resolution of output signals :returns: The output signal timestep in seconds. :rtype: dtm

<span id="ibmbackend-id-warning-issued" />

### id\_warning\_issued

<span id="qiskit_ibm_provider.IBMBackend.id_warning_issued" />

`= False`

<span id="ibmbackend-instruction-durations" />

### instruction\_durations

Return the [`InstructionDurations`](/api/qiskit/qiskit.transpiler.InstructionDurations.html#qiskit.transpiler.InstructionDurations "(in Qiskit v0.44)") object.

<span id="ibmbackend-instruction-schedule-map" />

### instruction\_schedule\_map

Return the [`InstructionScheduleMap`](/api/qiskit/qiskit.pulse.InstructionScheduleMap.html#qiskit.pulse.InstructionScheduleMap "(in Qiskit v0.44)") for the instructions defined in this backend’s target.

<span id="ibmbackend-instructions" />

### instructions

<span id="qiskit_ibm_provider.IBMBackend.instructions" />

`List[Tuple[Instruction, Tuple[int]]]`

A list of Instruction tuples on the backend of the form `(instruction, (qubits)`

**Return type**

`List`\[`Tuple`\[[`Instruction`](/api/qiskit/qiskit.circuit.Instruction.html#qiskit.circuit.Instruction "(in Qiskit v0.44)"), `Tuple`\[`int`]]]

<span id="ibmbackend-max-circuits" />

### max\_circuits

<span id="qiskit_ibm_provider.IBMBackend.max_circuits" />

`int`

The maximum number of circuits The maximum number of circuits that can be run in a single job. If there is no limit this will return None.

**Return type**

`int`

<span id="ibmbackend-meas-map" />

### meas\_map

<span id="qiskit_ibm_provider.IBMBackend.meas_map" />

`List[List[int]]`

Return the grouping of measurements which are multiplexed This is required to be implemented if the backend supports Pulse scheduling. :returns: The grouping of measurements which are multiplexed :rtype: meas\_map

<span id="ibmbackend-num-qubits" />

### num\_qubits

<span id="qiskit_ibm_provider.IBMBackend.num_qubits" />

`int`

Return the number of qubits the backend has.

**Return type**

`int`

<span id="ibmbackend-operation-names" />

### operation\_names

<span id="qiskit_ibm_provider.IBMBackend.operation_names" />

`List[str]`

A list of instruction names that the backend supports.

**Return type**

`List`\[`str`]

<span id="ibmbackend-operations" />

### operations

<span id="qiskit_ibm_provider.IBMBackend.operations" />

`List[Instruction]`

A list of [`Instruction`](/api/qiskit/qiskit.circuit.Instruction.html#qiskit.circuit.Instruction "(in Qiskit v0.44)") instances that the backend supports.

**Return type**

`List`\[[`Instruction`](/api/qiskit/qiskit.circuit.Instruction.html#qiskit.circuit.Instruction "(in Qiskit v0.44)")]

<span id="ibmbackend-options" />

### options

Return the options for the backend

The options of a backend are the dynamic parameters defining how the backend is used. These are used to control the [`run()`](qiskit_ibm_provider.IBMBackend#run "qiskit_ibm_provider.IBMBackend.run") method.

<span id="ibmbackend-provider" />

### provider

Return the backend Provider.

**Returns**

the Provider responsible for the backend.

**Return type**

Provider

<span id="ibmbackend-session" />

### session

<span id="qiskit_ibm_provider.IBMBackend.session" />

`Session`

Return session

**Return type**

[`Session`](qiskit_ibm_provider.Session "qiskit_ibm_provider.session.Session")

<span id="ibmbackend-target" />

### target

<span id="qiskit_ibm_provider.IBMBackend.target" />

`Target`

A [`qiskit.transpiler.Target`](/api/qiskit/qiskit.transpiler.Target.html#qiskit.transpiler.Target "(in Qiskit v0.44)") object for the backend. :rtype: [`Target`](/api/qiskit/qiskit.transpiler.Target.html#qiskit.transpiler.Target "(in Qiskit v0.44)") :returns: Target

<span id="ibmbackend-version" />

### version

<span id="qiskit_ibm_provider.IBMBackend.version" />

`= 2`

## Methods

<span id="ibmbackend-acquire-channel" />

### acquire\_channel

<span id="qiskit_ibm_provider.IBMBackend.acquire_channel" />

`IBMBackend.acquire_channel(qubit)`

Return the acquisition channel for the given qubit.

**Returns**

The Qubit measurement acquisition line.

**Return type**

AcquireChannel

<span id="ibmbackend-cancel-session" />

### cancel\_session

<span id="qiskit_ibm_provider.IBMBackend.cancel_session" />

`IBMBackend.cancel_session()`

Cancel session. All pending jobs will be cancelled.

**Return type**

`None`

<span id="ibmbackend-configuration" />

### configuration

<span id="qiskit_ibm_provider.IBMBackend.configuration" />

`IBMBackend.configuration()`

Return the backend configuration.

Backend configuration contains fixed information about the backend, such as its name, number of qubits, basis gates, coupling map, quantum volume, etc.

The schema for backend configuration can be found in [Qiskit/ibm-quantum-schemas](https://github.com/Qiskit/ibm-quantum-schemas/blob/main/schemas/backend_configuration_schema.json).

**Return type**

`Union`\[[`QasmBackendConfiguration`](/api/qiskit/qiskit.providers.models.QasmBackendConfiguration.html#qiskit.providers.models.QasmBackendConfiguration "(in Qiskit v0.44)"), [`PulseBackendConfiguration`](/api/qiskit/qiskit.providers.models.PulseBackendConfiguration.html#qiskit.providers.models.PulseBackendConfiguration "(in Qiskit v0.44)")]

**Returns**

The configuration for the backend.

<span id="ibmbackend-control-channel" />

### control\_channel

<span id="qiskit_ibm_provider.IBMBackend.control_channel" />

`IBMBackend.control_channel(qubits)`

Return the secondary drive channel for the given qubit.

This is typically utilized for controlling multiqubit interactions. This channel is derived from other channels.

**Parameters**

**qubits** (`Iterable`\[`int`]) – Tuple or list of qubits of the form `(control_qubit, target_qubit)`.

**Returns**

The Qubit measurement acquisition line.

**Return type**

List\[ControlChannel]

<span id="ibmbackend-defaults" />

### defaults

<span id="qiskit_ibm_provider.IBMBackend.defaults" />

`IBMBackend.defaults(refresh=False)`

Return the pulse defaults for the backend.

The schema for default pulse configuration can be found in [Qiskit/ibm-quantum-schemas](https://github.com/Qiskit/ibm-quantum-schemas/blob/main/schemas/default_pulse_configuration_schema.json).

**Parameters**

**refresh** (`bool`) – If `True`, re-query the server for the backend pulse defaults. Otherwise, return a cached version.

**Return type**

`Optional`\[[`PulseDefaults`](/api/qiskit/qiskit.providers.models.PulseDefaults.html#qiskit.providers.models.PulseDefaults "(in Qiskit v0.44)")]

**Returns**

The backend pulse defaults or `None` if the backend does not support pulse.

<span id="ibmbackend-drive-channel" />

### drive\_channel

<span id="qiskit_ibm_provider.IBMBackend.drive_channel" />

`IBMBackend.drive_channel(qubit)`

Return the drive channel for the given qubit.

**Returns**

The Qubit drive channel

**Return type**

DriveChannel

<span id="ibmbackend-get-translation-stage-plugin" />

### get\_translation\_stage\_plugin

<span id="qiskit_ibm_provider.IBMBackend.get_translation_stage_plugin" />

`classmethod IBMBackend.get_translation_stage_plugin()`

Return the default translation stage plugin name for IBM backends.

**Return type**

`str`

<span id="ibmbackend-measure-channel" />

### measure\_channel

<span id="qiskit_ibm_provider.IBMBackend.measure_channel" />

`IBMBackend.measure_channel(qubit)`

Return the measure stimulus channel for the given qubit.

**Returns**

The Qubit measurement stimulus line

**Return type**

MeasureChannel

<span id="ibmbackend-open-session" />

### open\_session

<span id="qiskit_ibm_provider.IBMBackend.open_session" />

`IBMBackend.open_session(max_time=None)`

Open session

**Return type**

[`Session`](qiskit_ibm_provider.Session "qiskit_ibm_provider.session.Session")

<span id="ibmbackend-properties" />

### properties

<span id="qiskit_ibm_provider.IBMBackend.properties" />

`IBMBackend.properties(refresh=False, datetime=None)`

Return the backend properties, subject to optional filtering.

This data describes qubits properties (such as T1 and T2), gates properties (such as gate length and error), and other general properties of the backend.

The schema for backend properties can be found in [Qiskit/ibm-quantum-schemas](https://github.com/Qiskit/ibm-quantum-schemas/blob/main/schemas/backend_properties_schema.json).

**Parameters**

*   **refresh** (`bool`) – If `True`, re-query the server for the backend properties. Otherwise, return a cached version.
*   **datetime** (`Optional`\[`datetime`]) – By specifying datetime, this function returns an instance of the [`BackendProperties`](/api/qiskit/qiskit.providers.models.BackendProperties.html#qiskit.providers.models.BackendProperties "(in Qiskit v0.44)") whose timestamp is closest to, but older than, the specified datetime.

**Return type**

`Optional`\[[`BackendProperties`](/api/qiskit/qiskit.providers.models.BackendProperties.html#qiskit.providers.models.BackendProperties "(in Qiskit v0.44)")]

**Returns**

The backend properties or `None` if the backend properties are not currently available.

**Raises**

**TypeError** – If an input argument is not of the correct type.

<span id="ibmbackend-qubit-properties" />

### qubit\_properties

<span id="qiskit_ibm_provider.IBMBackend.qubit_properties" />

`IBMBackend.qubit_properties(qubit)`

Return QubitProperties for a given qubit.

If there are no defined or the backend doesn’t support querying these details this method does not need to be implemented.

**Parameters**

**qubit** (`Union`\[`int`, `List`\[`int`]]) – The qubit to get the `QubitProperties` object for. This can be a single integer for 1 qubit or a list of qubits and a list of `QubitProperties` objects will be returned in the same order

**Returns**

The `QubitProperties` object for the specified qubit. If a list of qubits is provided a list will be returned. If properties are missing for a qubit this can be `None`.

**Return type**

qubit\_properties

**Raises**

**NotImplementedError** – if the backend doesn’t support querying the qubit properties

<span id="ibmbackend-run" />

### run

<span id="qiskit_ibm_provider.IBMBackend.run" />

`IBMBackend.run(circuits, dynamic=None, job_tags=None, init_circuit=None, init_num_resets=None, header=None, shots=None, memory=None, meas_level=None, meas_return=None, rep_delay=None, init_qubits=None, use_measure_esp=None, noise_model=None, seed_simulator=None, **run_config)`

Run on the backend. If a keyword specified here is also present in the `options` attribute/object, the value specified here will be used for this run.

**Parameters**

*   **circuits** (`Union`\[[`QuantumCircuit`](/api/qiskit/qiskit.circuit.QuantumCircuit.html#qiskit.circuit.QuantumCircuit "(in Qiskit v0.44)"), `str`, `List`\[`Union`\[[`QuantumCircuit`](/api/qiskit/qiskit.circuit.QuantumCircuit.html#qiskit.circuit.QuantumCircuit "(in Qiskit v0.44)"), `str`]]]) – An individual or a list of `QuantumCircuit`.

*   **dynamic** (`Optional`\[`bool`]) – Whether the circuit is dynamic (uses in-circuit conditionals)

*   **job\_tags** (`Optional`\[`List`\[`str`]]) – Tags to be assigned to the job. The tags can subsequently be used as a filter in the `jobs()` function call.

*   **init\_circuit** (`Optional`\[[`QuantumCircuit`](/api/qiskit/qiskit.circuit.QuantumCircuit.html#qiskit.circuit.QuantumCircuit "(in Qiskit v0.44)")]) – A quantum circuit to execute for initializing qubits before each circuit. If specified, `init_num_resets` is ignored. Applicable only if `dynamic=True` is specified.

*   **init\_num\_resets** (`Optional`\[`int`]) – The number of qubit resets to insert before each circuit execution.

*   **or** (*The following parameters are applicable only if dynamic=False is specified*) –

*   **to.** (*defaulted*) –

*   **header** (`Optional`\[`Dict`]) – User input that will be attached to the job and will be copied to the corresponding result header. Headers do not affect the run. This replaces the old `Qobj` header.

*   **shots** (`Union`\[`int`, `float`, `None`]) – Number of repetitions of each circuit, for sampling. Default: 4000 or `max_shots` from the backend configuration, whichever is smaller.

*   **memory** (`Optional`\[`bool`]) – If `True`, per-shot measurement bitstrings are returned as well (provided the backend supports it). For OpenPulse jobs, only measurement level 2 supports this option.

*   **meas\_level** (`Union`\[`int`, `MeasLevel`, `None`]) –

    Level of the measurement output for pulse experiments. See [OpenPulse specification](https://arxiv.org/pdf/1809.03452.pdf) for details:

    *   `0`, measurements of the raw signal (the measurement output pulse envelope)
    *   `1`, measurement kernel is selected (a complex number obtained after applying the measurement kernel to the measurement output signal)
    *   `2` (default), a discriminator is selected and the qubit state is stored (0 or 1)

*   **meas\_return** (`Union`\[`str`, `MeasReturnType`, `None`]) –

    Level of measurement data for the backend to return. For `meas_level` 0 and 1:

    *   `single` returns information from every shot.
    *   `avg` returns average measurement output (averaged over number of shots).

*   **rep\_delay** (`Optional`\[`float`]) – Delay between programs in seconds. Only supported on certain backends (if `backend.configuration().dynamic_reprate_enabled=True`). If supported, `rep_delay` must be from the range supplied by the backend (`backend.configuration().rep_delay_range`). Default is given by `backend.configuration().default_rep_delay`.

*   **init\_qubits** (`Optional`\[`bool`]) – Whether to reset the qubits to the ground state for each shot. Default: `True`.

*   **use\_measure\_esp** (`Optional`\[`bool`]) – Whether to use excited state promoted (ESP) readout for measurements which are the terminal instruction to a qubit. ESP readout can offer higher fidelity than standard measurement sequences. See [here](https://arxiv.org/pdf/2008.08571.pdf). Default: `True` if backend supports ESP readout, else `False`. Backend support for ESP readout is determined by the flag `measure_esp_enabled` in `backend.configuration()`.

*   **noise\_model** (`Optional`\[`Any`]) – Noise model. (Simulators only)

*   **seed\_simulator** (`Optional`\[`int`]) – Random seed to control sampling. (Simulators only)

*   **\*\*run\_config** – Extra arguments used to configure the run.

**Return type**

`IBMJob`

**Returns**

The job to be executed.

**Raises**

*   [**IBMBackendApiError**](qiskit_ibm_provider.IBMBackendApiError "qiskit_ibm_provider.IBMBackendApiError") – If an unexpected error occurred while submitting the job.

*   [**IBMBackendApiProtocolError**](qiskit_ibm_provider.IBMBackendApiProtocolError "qiskit_ibm_provider.IBMBackendApiProtocolError") – If an unexpected value received from the server.

*   [**IBMBackendValueError**](qiskit_ibm_provider.IBMBackendValueError "qiskit_ibm_provider.IBMBackendValueError") –

    *   If an input parameter value is not valid. - If ESP readout is used and the backend does not support this.

<span id="ibmbackend-set-options" />

### set\_options

<span id="qiskit_ibm_provider.IBMBackend.set_options" />

`IBMBackend.set_options(**fields)`

Set the options fields for the backend

This method is used to update the options of a backend. If you need to change any of the options prior to running just pass in the kwarg with the new value for the options.

**Parameters**

**fields** – The fields to update the options

**Raises**

**AttributeError** – If the field passed in is not part of the options

<span id="ibmbackend-status" />

### status

<span id="qiskit_ibm_provider.IBMBackend.status" />

`IBMBackend.status()`

Return the backend status.

<Admonition title="Note" type="note">
  If the returned [`BackendStatus`](/api/qiskit/qiskit.providers.models.BackendStatus.html#qiskit.providers.models.BackendStatus "(in Qiskit v0.44)") instance has `operational=True` but `status_msg="internal"`, then the backend is accepting jobs but not processing them.
</Admonition>

**Return type**

[`BackendStatus`](/api/qiskit/qiskit.providers.models.BackendStatus.html#qiskit.providers.models.BackendStatus "(in Qiskit v0.44)")

**Returns**

The status of the backend.

**Raises**

[**IBMBackendApiProtocolError**](qiskit_ibm_provider.IBMBackendApiProtocolError "qiskit_ibm_provider.IBMBackendApiProtocolError") – If the status for the backend cannot be formatted properly.

<span id="ibmbackend-target-history" />

### target\_history

<span id="qiskit_ibm_provider.IBMBackend.target_history" />

`IBMBackend.target_history(datetime=None)`

A [`qiskit.transpiler.Target`](/api/qiskit/qiskit.transpiler.Target.html#qiskit.transpiler.Target "(in Qiskit v0.44)") object for the backend. :rtype: [`Target`](/api/qiskit/qiskit.transpiler.Target.html#qiskit.transpiler.Target "(in Qiskit v0.44)") :returns: Target with properties found on datetime

