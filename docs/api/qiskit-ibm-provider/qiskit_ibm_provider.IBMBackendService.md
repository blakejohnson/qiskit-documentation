---
title: IBMBackendService
description: API reference for qiskit_ibm_provider.IBMBackendService
in_page_toc_min_heading_level: 1
python_api_type: class
python_api_name: qiskit_ibm_provider.IBMBackendService
---

# IBMBackendService

<span id="qiskit_ibm_provider.IBMBackendService" />

`IBMBackendService(provider, hgp)`

Backend namespace for an IBM Quantum account.

Represent a namespace that provides backend related services for the IBM Quantum backends available to this account. An instance of this class is used as a callable attribute to the [`IBMProvider`](qiskit_ibm_provider.IBMProvider "qiskit_ibm_provider.IBMProvider") class. This allows a convenient way to query for all backends or to access a specific backend:

```python
backends = provider.backends()  # Invoke backends() to get the backends.
sim_backend = provider.backend.ibmq_qasm_simulator  # Get a specific backend instance.
```

Also, you are able to retrieve jobs from an account without specifying the backend name. For example, to retrieve the ten most recent jobs you have submitted, regardless of the backend they were submitted to, you could do:

```python
most_recent_jobs = provider.backend.jobs(limit=10)
```

It is also possible to retrieve a single job without specifying the backend name:

```python
job = provider.backend.retrieve_job(<JOB_ID>)
```

IBMBackendService constructor.

**Parameters**

*   **provider** ([`IBMProvider`](qiskit_ibm_provider.IBMProvider "qiskit_ibm_provider.ibm_provider.IBMProvider")) – IBM Quantum account provider.
*   **hgp** (`HubGroupProject`) – default hub/group/project to use for the service.

## Methods

<span id="ibmbackendservice-backends" />

### backends

<span id="qiskit_ibm_provider.IBMBackendService.backends" />

`IBMBackendService.backends(name=None, filters=None, min_num_qubits=None, instance=None, dynamic_circuits=None, **kwargs)`

Return all backends accessible via this account, subject to optional filtering.

**Parameters**

*   **name** (`Optional`\[`str`]) – Backend name to filter by.

*   **min\_num\_qubits** (`Optional`\[`int`]) – Minimum number of qubits the backend must have.

*   **instance** (`Optional`\[`str`]) – The provider in the hub/group/project format.

*   **dynamic\_circuits** (`Optional`\[`bool`]) – Filter by whether the backend supports dynamic circuits.

*   **filters** (`Optional`\[`Callable`\[\[`List`\[[`IBMBackend`](qiskit_ibm_provider.IBMBackend "qiskit_ibm_provider.ibm_backend.IBMBackend")]], `bool`]]) –

    More complex filters, such as lambda functions. For example:

    ```python
    IBMProvider.backends(filters=lambda b: b.max_shots > 50000)
    IBMProvider.backends(filters=lambda x: ("rz" in x.basis_gates )
    ```

*   **\*\*kwargs** –

    Simple filters that require a specific value for an attribute in backend configuration, backend status, or provider credentials.

    Examples:

    ```python
    # Get the operational real backends
    IBMProvider.backends(simulator=False, operational=True)
    # Get the backends with at least 127 qubits
    IBMProvider.backends(min_num_qubits=127)
    # Get the backends that support OpenPulse
    IBMProvider.backends(open_pulse=True)
    ```

    For the full list of backend attributes, see the IBMBackend class documentation \<[providers\_models](/api/qiskit/providers_models)>

**Return type**

`List`\[[`IBMBackend`](qiskit_ibm_provider.IBMBackend "qiskit_ibm_provider.ibm_backend.IBMBackend")]

**Returns**

The list of available backends that match the filter.

**Raises**

*   [**IBMBackendValueError**](qiskit_ibm_provider.IBMBackendValueError "qiskit_ibm_provider.IBMBackendValueError") – If only one or two parameters from hub, group, project are specified.
*   **QiskitBackendNotFoundError** – If the backend is not found in any instance.

<span id="ibmbackendservice-jobs" />

### jobs

<span id="qiskit_ibm_provider.IBMBackendService.jobs" />

`IBMBackendService.jobs(limit=10, skip=0, backend_name=None, status=None, start_datetime=None, end_datetime=None, job_tags=None, descending=True, instance=None, legacy=False)`

Return a list of jobs, subject to optional filtering.

Retrieve jobs that match the given filters and paginate the results if desired. Note that the server has a limit for the number of jobs returned in a single call. As a result, this function might involve making several calls to the server.

**Parameters**

*   **limit** (`Optional`\[`int`]) – Number of jobs to retrieve. `None` means no limit. Note that the number of sub-jobs within a composite job count towards the limit.
*   **skip** (`int`) – Starting index for the job retrieval.
*   **backend\_name** (`Optional`\[`str`]) – Name of the backend to retrieve jobs from.
*   **status** (`Union`\[`Literal`\[‘pending’, ‘completed’], `List`\[`Union`\[[`JobStatus`](/api/qiskit/qiskit.providers.JobStatus.html#qiskit.providers.JobStatus "(in Qiskit v0.44)"), `str`]], [`JobStatus`](/api/qiskit/qiskit.providers.JobStatus.html#qiskit.providers.JobStatus "(in Qiskit v0.44)"), `str`, `None`]) – Filter jobs with either “pending” or “completed” status. You can also specify by
*   **example** (*exact status. For*) – or status=\[“RUNNING”, “ERROR”].
*   **status="RUNNING"** (*status=JobStatus.RUNNING or*) – or status=\[“RUNNING”, “ERROR”].
*   **start\_datetime** (`Optional`\[`datetime`]) – Filter by the given start date, in local time. This is used to find jobs whose creation dates are after (greater than or equal to) this local date/time.
*   **end\_datetime** (`Optional`\[`datetime`]) – Filter by the given end date, in local time. This is used to find jobs whose creation dates are before (less than or equal to) this local date/time.
*   **job\_tags** (`Optional`\[`List`\[`str`]]) – Filter by tags assigned to jobs. Matched jobs are associated with all tags.
*   **descending** (`bool`) – If `True`, return the jobs in descending order of the job creation date (i.e. newest first) until the limit is reached.
*   **instance** (`Optional`\[`str`]) – The provider in the hub/group/project format.
*   **legacy** (`bool`) – If `True`, only retrieve jobs run from the archived `qiskit-ibmq-provider`.
*   **Otherwise** –
*   **qiskit-ibm-provider.** (*only retrieve jobs run from*) –

**Return type**

`List`\[`IBMJob`]

**Returns**

A list of `IBMJob` instances.

**Raises**

*   [**IBMBackendValueError**](qiskit_ibm_provider.IBMBackendValueError "qiskit_ibm_provider.IBMBackendValueError") – If a keyword value is not recognized.
*   **TypeError** – If the input start\_datetime or end\_datetime parameter value is not valid.

<span id="ibmbackendservice-retrieve-job" />

### retrieve\_job

<span id="qiskit_ibm_provider.IBMBackendService.retrieve_job" />

`IBMBackendService.retrieve_job(job_id)`

Return a single job.

**Parameters**

**job\_id** (`str`) – The ID of the job to retrieve.

**Return type**

`IBMJob`

**Returns**

The job with the given id.

**Raises**

*   [**IBMBackendApiError**](qiskit_ibm_provider.IBMBackendApiError "qiskit_ibm_provider.IBMBackendApiError") – If an unexpected error occurred when retrieving the job.
*   [**IBMBackendApiProtocolError**](qiskit_ibm_provider.IBMBackendApiProtocolError "qiskit_ibm_provider.IBMBackendApiProtocolError") – If unexpected return value received from the server.
*   **IBMJobNotFoundError** – If job cannot be found.
*   **IBMInputValueError** – If job exists but was run from a different service.

