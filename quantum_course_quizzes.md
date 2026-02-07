# Quantum Course - Sample Quizzes with Answer Keys

## Week 1 Quiz: Quantum Computing Fundamentals & Hardware Architecture

**Question 1:** Which qubit technology typically operates at millikelvin temperatures?
a) Photonic qubits
b) Superconducting qubits
c) Neutral atom qubits
d) NV center qubits

**Answer: b) Superconducting qubits**

---

**Question 2:** What is the primary cause of decoherence in quantum systems?
a) Interaction with the environment
b) Gate errors
c) Power fluctuations
d) Software bugs

**Answer: a) Interaction with the environment**

---

**Question 3:** In the quantum software stack, which layer is responsible for translating high-level algorithms into hardware-specific instructions?
a) Application layer
b) Compiler/Middleware layer
c) Control layer
d) Hardware layer

**Answer: b) Compiler/Middleware layer**

---

**Question 4:** What quantum phenomenon allows a qubit to exist in multiple states simultaneously?
a) Entanglement
b) Interference
c) Superposition
d) Tunneling

**Answer: c) Superposition**

---

**Question 5:** Which of the following is NOT a common quantum gate?
a) Hadamard (H)
b) CNOT
c) XOR
d) Pauli-X

**Answer: c) XOR (this is classical, not quantum)**

---

**Question 6:** What is the typical coherence time (T2) for state-of-the-art superconducting qubits?
a) Nanoseconds
b) Microseconds to hundreds of microseconds
c) Milliseconds
d) Seconds

**Answer: b) Microseconds to hundreds of microseconds**

---

**Question 7:** In ion trap quantum computers, what is primarily used to manipulate qubits?
a) Microwave pulses
b) Laser pulses
c) Magnetic fields
d) Electric currents

**Answer: b) Laser pulses**

---

**Question 8:** What does the Bloch sphere represent?
a) The physical location of a qubit
b) The quantum state of a single qubit
c) The entanglement structure
d) The error rate

**Answer: b) The quantum state of a single qubit**

---

**Question 9:** Which quantum property allows two qubits to be correlated regardless of distance?
a) Superposition
b) Interference
c) Entanglement
d) Decoherence

**Answer: c) Entanglement**

---

**Question 10:** What is a major challenge in scaling quantum computers?
a) Maintaining qubit connectivity while controlling cross-talk
b) Increasing classical computer power
c) Finding enough physicists
d) Patent restrictions

**Answer: a) Maintaining qubit connectivity while controlling cross-talk**

---

## Week 2 Quiz: Quantum Control Software & Pulse Engineering

**Question 1:** What is the purpose of DRAG (Derivative Removal by Adiabatic Gate) pulses?
a) To increase gate speed
b) To reduce leakage to non-computational states
c) To improve measurement fidelity
d) To reduce cross-talk

**Answer: b) To reduce leakage to non-computational states**

---

**Question 2:** Which component converts digital signals into analog control waveforms?
a) ADC
b) DAC
c) FPGA
d) CPU

**Answer: b) DAC (Digital-to-Analog Converter)**

---

**Question 3:** What is the typical frequency range for microwave control of superconducting qubits?
a) 1-10 MHz
b) 100-500 MHz
c) 3-8 GHz
d) 50-100 GHz

**Answer: c) 3-8 GHz**

---

**Question 4:** In Qiskit Pulse, what does a Schedule object represent?
a) A quantum circuit
b) A sequence of timed pulse instructions
c) A compilation strategy
d) A measurement protocol

**Answer: b) A sequence of timed pulse instructions**

---

**Question 5:** What is the primary purpose of pulse shaping in quantum control?
a) To reduce power consumption
b) To minimize spectral leakage and unwanted transitions
c) To increase measurement speed
d) To simplify hardware design

**Answer: b) To minimize spectral leakage and unwanted transitions**

---

**Question 6:** What does an Arbitrary Waveform Generator (AWG) do?
a) Measures quantum states
b) Generates custom analog waveforms for qubit control
c) Amplifies signals
d) Filters noise

**Answer: b) Generates custom analog waveforms for qubit control**

---

**Question 7:** Why is timing synchronization critical in quantum control?
a) To reduce power consumption
b) To ensure gates are applied at the correct times and phases
c) To improve software performance
d) To simplify calibration

**Answer: b) To ensure gates are applied at the correct times and phases**

---

**Question 8:** What is the OpenPulse framework?
a) A hardware specification for quantum computers
b) An open-source standard for pulse-level quantum control
c) A calibration algorithm
d) A quantum error correction code

**Answer: b) An open-source standard for pulse-level quantum control**

---

**Question 9:** What determines the duration of a single-qubit gate pulse?
a) Only the desired rotation angle
b) Trade-off between speed and fidelity
c) The qubit's T1 time only
d) Software optimization

**Answer: b) Trade-off between speed and fidelity**

---

**Question 10:** What is flux biasing used for in superconducting qubits?
a) Measurement
b) Tuning qubit frequency
c) Error correction
d) Cooling

**Answer: b) Tuning qubit frequency**

---

## Week 3 Quiz: Calibration & Characterization Software

**Question 1:** What does randomized benchmarking primarily measure?
a) Qubit coherence time
b) Average gate fidelity
c) Measurement error
d) Cross-talk

**Answer: b) Average gate fidelity**

---

**Question 2:** Why is automated calibration important in quantum systems?
a) Qubit parameters drift over time
b) It's legally required
c) To reduce energy consumption
d) To simplify user interfaces

**Answer: a) Qubit parameters drift over time**

---

**Question 3:** What is quantum process tomography used for?
a) Measuring qubit states
b) Fully characterizing a quantum gate or process
c) Optimizing circuits
d) Detecting hardware failures

**Answer: b) Fully characterizing a quantum gate or process**

---

**Question 4:** In gate calibration, what parameter is typically optimized for a single-qubit rotation?
a) Pulse amplitude and duration
b) Qubit temperature
c) Measurement time
d) Compiler settings

**Answer: a) Pulse amplitude and duration**

---

**Question 5:** What does cross-talk characterization measure?
a) Communication between qubits
b) Unwanted interactions between qubit control lines
c) Classical-quantum correlation
d) User satisfaction

**Answer: b) Unwanted interactions between qubit control lines**

---

**Question 6:** What is the primary advantage of automated calibration routines?
a) Reduced human error and faster optimization
b) Lower equipment costs
c) Simplified physics
d) Reduced power consumption

**Answer: a) Reduced human error and faster optimization**

---

**Question 7:** What does gate set tomography provide?
a) Circuit optimization suggestions
b) Complete characterization of a set of quantum gates
c) Hardware design recommendations
d) Cost estimates

**Answer: b) Complete characterization of a set of quantum gates**

---

**Question 8:** Which metric is most commonly used to evaluate two-qubit gate quality?
a) Speed
b) Fidelity
c) Power consumption
d) Cost

**Answer: b) Fidelity**

---

**Question 9:** What is a typical target fidelity for two-qubit gates in modern superconducting systems?
a) 50-60%
b) 70-80%
c) 90-95%
d) 99%+

**Answer: d) 99%+ (99.0-99.5% is state-of-the-art)**

---

**Question 10:** How often do qubit parameters typically need recalibration?
a) Once per year
b) Daily to weekly
c) Every few hours
d) Continuously in real-time

**Answer: b) Daily to weekly (though some systems may need more frequent calibration)**

---

## Week 4 Quiz: Real-Time Control Systems

**Question 1:** What is the primary advantage of using FPGAs for quantum control?
a) Low cost
b) Deterministic, low-latency processing
c) Easy programming
d) High memory capacity

**Answer: b) Deterministic, low-latency processing**

---

**Question 2:** What is mid-circuit measurement?
a) Measuring all qubits halfway through a circuit
b) Measuring specific qubits during circuit execution (not just at the end)
c) Approximate measurement
d) Measurement without destroying the quantum state

**Answer: b) Measuring specific qubits during circuit execution (not just at the end)**

---

**Question 3:** What is the typical latency requirement for feedback in quantum error correction?
a) Seconds
b) Milliseconds
c) Microseconds
d) Nanoseconds

**Answer: c) Microseconds**

---

**Question 4:** What is active qubit reset?
a) Restarting the quantum computer
b) Quickly preparing a qubit in the ground state after measurement
c) Cooling the system
d) Recalibrating gates

**Answer: b) Quickly preparing a qubit in the ground state after measurement**

---

**Question 5:** In FPGA programming for quantum control, what language is commonly used?
a) Python
b) JavaScript
c) VHDL or Verilog
d) Ruby

**Answer: c) VHDL or Verilog**

---

**Question 6:** Why is low latency critical for quantum feedback?
a) To reduce costs
b) To implement quantum error correction before decoherence
c) To improve user experience
d) To simplify programming

**Answer: b) To implement quantum error correction before decoherence**

---

**Question 7:** What role does classical control play in quantum error correction?
a) No role - it's purely quantum
b) Processing syndrome measurements and determining corrections
c) Only data logging
d) Only visualization

**Answer: b) Processing syndrome measurements and determining corrections**

---

**Question 8:** What is a key challenge in implementing real-time feedback loops?
a) Software licensing
b) Meeting tight timing constraints while processing measurement data
c) User interface design
d) Documentation

**Answer: b) Meeting tight timing constraints while processing measurement data**

---

**Question 9:** What does conditional operation based on measurement enable?
a) Faster gates
b) Quantum teleportation and error correction
c) Cheaper hardware
d) Simpler circuits

**Answer: b) Quantum teleportation and error correction**

---

**Question 10:** What is the advantage of high-level synthesis (HLS) for FPGA programming?
a) Better performance than HDL
b) Easier development using C/C++-like languages
c) Lower cost
d) No advantage

**Answer: b) Easier development using C/C++-like languages**

---

## Week 5 Quiz: Quantum Compilers & Transpilation

**Question 1:** What is the main purpose of quantum circuit transpilation?
a) Converting circuits to run on specific hardware constraints
b) Making circuits faster classically
c) Reducing code size
d) Improving visualization

**Answer: a) Converting circuits to run on specific hardware constraints**

---

**Question 2:** What is gate decomposition?
a) Breaking down complex gates into hardware-native gates
b) Removing unnecessary gates
c) Combining gates
d) Measuring gates

**Answer: a) Breaking down complex gates into hardware-native gates**

---

**Question 3:** Why is qubit routing necessary?
a) To reduce errors
b) Limited qubit connectivity in hardware topologies
c) To speed up gates
d) For visualization

**Answer: b) Limited qubit connectivity in hardware topologies**

---

**Question 4:** What optimization does gate cancellation perform?
a) Removes gates that cancel each other out (e.g., XX = I)
b) Reduces gate amplitude
c) Combines all gates into one
d) Spreads gates evenly

**Answer: a) Removes gates that cancel each other out (e.g., XX = I)**

---

**Question 5:** What are basis gates?
a) The first gates in a circuit
b) The native gate set that hardware can directly implement
c) The most common gates
d) Gates with highest fidelity

**Answer: b) The native gate set that hardware can directly implement**

---

**Question 6:** What is the purpose of circuit optimization passes?
a) To reduce circuit depth and gate count while preserving functionality
b) To make circuits look nicer
c) To add more gates
d) To slow down execution

**Answer: a) To reduce circuit depth and gate count while preserving functionality**

---

**Question 7:** What does hardware-aware compilation consider?
a) Software preferences
b) Device topology, gate fidelities, and calibration data
c) User skill level
d) Historical data only

**Answer: b) Device topology, gate fidelities, and calibration data**

---

**Question 8:** What is commutation analysis in circuit optimization?
a) Identifying gates that can be reordered without changing the result
b) Removing all gates
c) Adding communication protocols
d) Measuring gate speed

**Answer: a) Identifying gates that can be reordered without changing the result**

---

**Question 9:** In Qiskit, what does the transpile() function do?
a) Only optimizes circuits
b) Translates circuits to hardware-compatible form with routing and optimization
c) Only routes qubits
d) Only validates circuits

**Answer: b) Translates circuits to hardware-compatible form with routing and optimization**

---

**Question 10:** What metric is typically minimized during compilation?
a) Number of qubits
b) Circuit depth (to reduce decoherence effects)
c) Developer time
d) Documentation length

**Answer: b) Circuit depth (to reduce decoherence effects)**

---

## Week 6 Quiz: Error Mitigation & Correction Software

**Question 1:** What is the difference between error mitigation and error correction?
a) No difference
b) Mitigation reduces errors probabilistically; correction uses redundancy to fix errors
c) Mitigation is hardware-based; correction is software-based
d) Mitigation is older technology

**Answer: b) Mitigation reduces errors probabilistically; correction uses redundancy to fix errors**

---

**Question 2:** What does Zero-Noise Extrapolation (ZNE) do?
a) Eliminates all noise
b) Extrapolates to zero-noise result by running at different noise levels
c) Adds noise to circuits
d) Measures noise only

**Answer: b) Extrapolates to zero-noise result by running at different noise levels**

---

**Question 3:** What is a stabilizer in quantum error correction?
a) Hardware component
b) An operator that commutes with the code space
c) A type of qubit
d) A measurement device

**Answer: b) An operator that commutes with the code space**

---

**Question 4:** What is the surface code?
a) A coating for qubits
b) A topological quantum error correction code
c) A programming language
d) A measurement technique

**Answer: b) A topological quantum error correction code**

---

**Question 5:** What is the primary purpose of a decoder in quantum error correction?
a) To encrypt data
b) To infer errors from syndrome measurements
c) To measure qubits
d) To compile circuits

**Answer: b) To infer errors from syndrome measurements**

---

**Question 6:** What is Probabilistic Error Cancellation (PEC)?
a) Removing all errors
b) Using inverse noise operations with probabilistic sampling
c) Ignoring small errors
d) Hardware filtering

**Answer: b) Using inverse noise operations with probabilistic sampling**

---

**Question 7:** What is the distance of a quantum error correction code?
a) Physical spacing between qubits
b) Minimum number of qubits that must be affected to cause a logical error
c) Code efficiency
d) Measurement accuracy

**Answer: b) Minimum number of qubits that must be affected to cause a logical error**

---

**Question 8:** What does MWPM stand for in the context of QEC decoders?
a) Maximum Weight Perfect Matching
b) Minimum Weight Perfect Matching
c) Multi-Way Pulse Modulation
d) Measured Wave Pattern Matching

**Answer: b) Minimum Weight Perfect Matching**

---

**Question 9:** What is a logical qubit?
a) A qubit used for logic gates
b) An encoded qubit protected by error correction
c) A theoretical qubit
d) A software simulation

**Answer: b) An encoded qubit protected by error correction**

---

**Question 10:** Why is error correction essential for fault-tolerant quantum computing?
a) To meet regulatory requirements
b) Physical qubits have error rates too high for long computations
c) To reduce costs
d) To simplify programming

**Answer: b) Physical qubits have error rates too high for long computations**

---

## Week 7 Quiz: Cryogenic & Classical Infrastructure Software

**Question 1:** What temperature do dilution refrigerators typically reach for superconducting qubits?
a) 4 Kelvin
b) 77 Kelvin
c) 10-20 millikelvin
d) Room temperature

**Answer: c) 10-20 millikelvin**

---

**Question 2:** Why is temperature monitoring critical in quantum systems?
a) For billing purposes
b) Temperature affects qubit coherence and gate fidelity
c) For comfort
d) Legal requirements

**Answer: b) Temperature affects qubit coherence and gate fidelity**

---

**Question 3:** What type of database is commonly used for time-series hardware monitoring data?
a) MySQL
b) MongoDB
c) InfluxDB
d) Oracle

**Answer: c) InfluxDB**

---

**Question 4:** What is the purpose of automated health checks in quantum systems?
a) To reduce insurance costs
b) To detect anomalies and prevent system failures
c) To entertain operators
d) To generate reports only

**Answer: b) To detect anomalies and prevent system failures**

---

**Question 5:** What does DAQ stand for?
a) Data Acquisition
b) Digital Analog Quality
c) Device Authentication Queue
d) Daily Analysis Query

**Answer: a) Data Acquisition**

---

**Question 6:** Why is vacuum system management important in quantum computing?
a) For cleanliness
b) To maintain thermal isolation and reduce noise
c) To save space
d) For aesthetics

**Answer: b) To maintain thermal isolation and reduce noise**

---

**Question 7:** What visualization tool is commonly used for real-time monitoring dashboards?
a) Microsoft Excel
b) Grafana
c) PowerPoint
d) Paint

**Answer: b) Grafana**

---

**Question 8:** What parameter is most critical to monitor in a dilution refrigerator?
a) Color
b) Mixing chamber temperature
c) Size
d) Weight

**Answer: b) Mixing chamber temperature**

---

**Question 9:** What is the purpose of automated alerting systems?
a) To wake up operators
b) To notify staff of critical system events requiring intervention
c) To play music
d) To test speakers

**Answer: b) To notify staff of critical system events requiring intervention**

---

**Question 10:** What type of data should be logged from quantum hardware?
a) Only errors
b) Temperature, pressure, gate fidelities, calibration data, errors
c) Only successful runs
d) User comments only

**Answer: b) Temperature, pressure, gate fidelities, calibration data, errors**

---

## Week 8 Quiz: Quantum Device Drivers & APIs

**Question 1:** What is a Hardware Abstraction Layer (HAL)?
a) A physical layer of the computer
b) Software that provides a consistent interface to different hardware
c) A type of qubit
d) A measurement protocol

**Answer: b) Software that provides a consistent interface to different hardware**

---

**Question 2:** What protocol is REST based on?
a) FTP
b) HTTP
c) SMTP
d) SSH

**Answer: b) HTTP**

---

**Question 3:** What is the purpose of a job queue in quantum computing systems?
a) To organize people waiting
b) To manage and prioritize quantum job submissions
c) To store data
d) To compile circuits

**Answer: b) To manage and prioritize quantum job submissions**

---

**Question 4:** What is OpenQASM?
a) A hardware component
b) An open quantum assembly language
c) A company name
d) A measurement technique

**Answer: b) An open quantum assembly language**

---

**Question 5:** Why is authentication important in cloud quantum systems?
a) To increase revenue
b) To control access and track usage
c) For decoration
d) It's not important

**Answer: b) To control access and track usage**

---

**Question 6:** What advantage does gRPC have over REST for some applications?
a) Older technology
b) More efficient binary serialization and bi-directional streaming
c) Easier to learn
d) No advantage

**Answer: b) More efficient binary serialization and bi-directional streaming**

---

**Question 7:** What is the role of a device driver?
a) To operate vehicles
b) To interface between software and hardware devices
c) To store data
d) To visualize results

**Answer: b) To interface between software and hardware devices**

---

**Question 8:** What information should an API return when a quantum job is submitted?
a) Only success/failure
b) Job ID for tracking status and retrieving results
c) Full results immediately
d) Nothing

**Answer: b) Job ID for tracking status and retrieving results**

---

**Question 9:** What is OpenQASM 3.0's improvement over 2.0?
a) No improvements
b) Real-time classical control flow and mid-circuit measurements
c) Just a version number change
d) Fewer features

**Answer: b) Real-time classical control flow and mid-circuit measurements**

---

**Question 10:** What should an API rate limit prevent?
a) Learning
b) System overload from excessive requests
c) Success
d) Measurement

**Answer: b) System overload from excessive requests**

---

## Week 9 Quiz: Quantum Algorithm Development Tools

**Question 1:** What does VQE stand for?
a) Variable Quantum Encoder
b) Variational Quantum Eigensolver
c) Very Quick Execution
d) Virtual Qubit Environment

**Answer: b) Variational Quantum Eigensolver**

---

**Question 2:** What is VQE primarily used for?
a) Error correction
b) Finding ground state energies of molecules
c) Compiling circuits
d) Measuring qubits

**Answer: b) Finding ground state energies of molecules**

---

**Question 3:** What does QAOA stand for?
a) Quantum Approximate Optimization Algorithm
b) Quick Algorithm Optimization Analysis
c) Quantum Advanced Operational Architecture
d) Qubit Amplitude Oscillation Approach

**Answer: a) Quantum Approximate Optimization Algorithm**

---

**Question 4:** What is a parameterized quantum circuit?
a) A circuit with fixed gates
b) A circuit with adjustable parameters optimized classically
c) A classical circuit
d) A measurement-only circuit

**Answer: b) A circuit with adjustable parameters optimized classically**

---

**Question 5:** What does NISQ stand for?
a) New Intelligent Superconducting Qubits
b) Noisy Intermediate-Scale Quantum
c) Next-generation Isolated Quantum Systems
d) Non-Interactive Scalable Qubits

**Answer: b) Noisy Intermediate-Scale Quantum**

---

**Question 6:** How are gradients typically calculated for variational quantum algorithms?
a) Numerical differentiation only
b) Parameter shift rule or finite differences
c) They're not needed
d) Random guessing

**Answer: b) Parameter shift rule or finite differences**

---

**Question 7:** What is an ansatz in the context of VQE?
a) A measurement outcome
b) The parameterized circuit structure used to prepare trial states
c) A type of qubit
d) An error

**Answer: b) The parameterized circuit structure used to prepare trial states**

---

**Question 8:** What is PennyLane?
a) A hardware manufacturer
b) A quantum machine learning framework
c) A type of qubit
d) A measurement device

**Answer: b) A quantum machine learning framework**

---

**Question 9:** Why are hardware-efficient ansätze important for NISQ devices?
a) They look nice
b) They use gates native to the hardware, reducing errors and circuit depth
c) They're easier to understand
d) They're required by law

**Answer: b) They use gates native to the hardware, reducing errors and circuit depth**

---

**Question 10:** What optimization challenge do VQAs face?
a) No challenges
b) Barren plateaus where gradients vanish
c) Too much memory
d) Legal restrictions

**Answer: b) Barren plateaus where gradients vanish**

---

## Week 10 Quiz: Testing, Validation & CI/CD

**Question 1:** What is unit testing in quantum software?
a) Testing physical units
b) Testing individual functions or components in isolation
c) Testing all code at once
d) Testing user interfaces

**Answer: b) Testing individual functions or components in isolation**

---

**Question 2:** Why is simulation important before running on actual quantum hardware?
a) It's not important
b) To validate logic and catch errors without consuming expensive hardware time
c) To slow down development
d) For entertainment

**Answer: b) To validate logic and catch errors without consuming expensive hardware time**

---

**Question 3:** What does CI/CD stand for?
a) Continuous Integration/Continuous Deployment
b) Computer Integration/Computer Development
c) Calibration Improvement/Code Distribution
d) Classical Implementation/Classical Development

**Answer: a) Continuous Integration/Continuous Deployment**

---

**Question 4:** What is the purpose of regression testing?
a) To slow down development
b) To ensure new changes don't break existing functionality
c) To test older code only
d) To remove features

**Answer: b) To ensure new changes don't break existing functionality**

---

**Question 5:** What is a typical target for code coverage in production software?
a) 10-20%
b) 40-50%
c) 70-90%
d) Coverage doesn't matter

**Answer: c) 70-90%**

---

**Question 6:** What should integration tests verify in quantum software?
a) Only individual functions
b) Interaction between different stack layers (control, middleware, API)
c) Nothing
d) Only UI

**Answer: b) Interaction between different stack layers (control, middleware, API)**

---

**Question 7:** What is the benefit of automated testing in CI/CD pipelines?
a) No benefit
b) Immediate feedback on code changes and prevention of bugs
c) Slower development
d) More meetings

**Answer: b) Immediate feedback on code changes and prevention of bugs**

---

**Question 8:** What should be version controlled in quantum systems?
a) Only source code
b) Source code, hardware configurations, and calibration parameters
c) Nothing
d) Only documentation

**Answer: b) Source code, hardware configurations, and calibration parameters**

---

**Question 9:** Why is documentation important in quantum software?
a) It's not important
b) Complexity of systems requires clear documentation for maintenance and collaboration
c) To increase file size
d) For decoration

**Answer: b) Complexity of systems requires clear documentation for maintenance and collaboration**

---

**Question 10:** What tool is commonly used for CI/CD in GitHub-based projects?
a) Microsoft Word
b) GitHub Actions
c) Paint
d) Excel

**Answer: b) GitHub Actions**

---

## Week 11 Quiz: Performance Optimization & Scalability

**Question 1:** What is the purpose of profiling software?
a) Creating user profiles
b) Identifying performance bottlenecks
c) Testing features
d) Writing documentation

**Answer: b) Identifying performance bottlenecks**

---

**Question 2:** What is a common bottleneck in calibration routines?
a) User interface
b) Sequential execution of calibration experiments
c) Documentation
d) Colors

**Answer: b) Sequential execution of calibration experiments**

---

**Question 3:** How can parallel processing improve quantum systems?
a) It can't
b) Running multiple independent experiments simultaneously
c) Slowing down execution
d) Reducing accuracy

**Answer: b) Running multiple independent experiments simultaneously**

---

**Question 4:** What challenge arises when scaling from 10 to 100+ qubits?
a) No challenges
b) Exponential growth in calibration complexity and cross-talk
c) Fewer challenges
d) Simpler systems

**Answer: b) Exponential growth in calibration complexity and cross-talk**

---

**Question 5:** Why is database optimization important for large quantum systems?
a) It's not important
b) Massive amounts of calibration and result data need efficient storage/retrieval
c) To use more disk space
d) For decoration

**Answer: b) Massive amounts of calibration and result data need efficient storage/retrieval**

---

**Question 6:** What is distributed compilation?
a) Compiling on one computer
b) Splitting compilation tasks across multiple compute nodes
c) Not compiling at all
d) Compiling slowly

**Answer: b) Splitting compilation tasks across multiple compute nodes**

---

**Question 7:** What memory consideration is important for large quantum circuits?
a) None
b) Statevector simulation requires exponential memory in qubit count
c) More is always better
d) Memory doesn't matter

**Answer: b) Statevector simulation requires exponential memory in qubit count**

---

**Question 8:** How can calibration be made more efficient?
a) Do it less often
b) Parallelize independent calibrations and use smart scheduling
c) Skip it entirely
d) Use slower methods

**Answer: b) Parallelize independent calibrations and use smart scheduling**

---

**Question 9:** What is a key principle in scalable system design?
a) Ignore scalability
b) Design with modularity and clear interfaces between components
c) Make everything coupled
d) Use only one programming language

**Answer: b) Design with modularity and clear interfaces between components**

---

**Question 10:** What tool can help identify slow code sections?
a) Text editor
b) Profiler (cProfile, line_profiler, etc.)
c) Calculator
d) Email client

**Answer: b) Profiler (cProfile, line_profiler, etc.)**

---

## Week 12 Quiz: Industry Standards & Integration

**Question 1:** What is the purpose of quantum computing standards?
a) To limit innovation
b) To enable interoperability and portability across platforms
c) To increase costs
d) For decoration

**Answer: b) To enable interoperability and portability across platforms**

---

**Question 2:** What organization is developing quantum computing standards?
a) Only private companies
b) IEEE, ISO, and other standards bodies
c) No one
d) Only governments

**Answer: b) IEEE, ISO, and other standards bodies**

---

**Question 3:** What is Quil?
a) A hardware component
b) A quantum instruction language developed by Rigetti
c) A measurement technique
d) A type of qubit

**Answer: b) A quantum instruction language developed by Rigetti**

---

**Question 4:** How can quantum systems integrate with classical HPC?
a) They can't
b) Hybrid algorithms using classical optimization with quantum subroutines
c) Replacing HPC entirely
d) No integration needed

**Answer: b) Hybrid algorithms using classical optimization with quantum subroutines**

---

**Question 5:** What is a hybrid quantum-classical workflow?
a) Using both quantum and classical computers in same algorithm
b) Running separate quantum and classical programs
c) Using quantum computers only
d) Using classical computers only

**Answer: a) Using both quantum and classical computers in same algorithm**

---

**Question 6:** Why is security important for quantum systems?
a) It's not important
b) To protect IP, control access, and secure sensitive computation results
c) For marketing
d) Legal requirement only

**Answer: b) To protect IP, control access, and secure sensitive computation results**

---

**Question 7:** What should a disaster recovery plan for quantum systems include?
a) Nothing
b) Data backup, configuration versioning, and recovery procedures
c) Only hardware replacement
d) Only software backups

**Answer: b) Data backup, configuration versioning, and recovery procedures**

---

**Question 8:** What is the advantage of standardized quantum languages?
a) No advantage
b) Code portability across different quantum platforms
c) Slower execution
d) More complex programming

**Answer: b) Code portability across different quantum platforms**

---

**Question 9:** What consideration is important for production deployment?
a) Aesthetics only
b) Reliability, monitoring, backup systems, and documentation
c) Speed only
d) Cost only

**Answer: b) Reliability, monitoring, backup systems, and documentation**

---

**Question 10:** How can quantum computing complement classical HPC?
a) It can't
b) Solving specific problems (optimization, simulation) faster than classical
c) Replacing it entirely
d) No relationship

**Answer: b) Solving specific problems (optimization, simulation) faster than classical**

---

## Capstone Project Evaluation Rubric

### Code Quality (20 points)
- Clean, well-organized code structure (5 pts)
- Proper documentation and comments (5 pts)
- Following Python/coding best practices (5 pts)
- Error handling and input validation (5 pts)

### Functionality (30 points)
- Hardware simulation accuracy (8 pts)
- Control software completeness (8 pts)
- Middleware/compilation working (7 pts)
- API functionality (7 pts)

### Performance (20 points)
- System responsiveness (5 pts)
- Scalability demonstration (5 pts)
- Resource optimization (5 pts)
- Stress test results (5 pts)

### Documentation (15 points)
- Architecture documentation (5 pts)
- API documentation (5 pts)
- User guide clarity (5 pts)

### Presentation (15 points)
- Clear explanation of architecture (5 pts)
- Effective live demonstration (5 pts)
- Professional delivery and Q&A (5 pts)

**Total: 100 points**

**Grading Scale:**
- 90-100: A (Excellent)
- 80-89: B (Good)
- 70-79: C (Satisfactory)
- Below 70: Incomplete

