# Week 1 Supplementary Materials
## Quantum Computing Fundamentals & Hardware Architecture

### Extended Content Companion to Main Document

---

## Section 1: In-Depth Hardware Analysis

### 1.1 Superconducting Qubit Deep Dive

#### 1.1.1 Transmon Qubit Architecture

The transmon (transmission line shunted plasma oscillation qubit) is the most widely used superconducting qubit design. It achieves longer coherence times by shunting the Josephson junction with a large capacitance, reducing charge noise sensitivity.

**Physical Construction:**
- Josephson junction: Two superconducting layers separated by thin insulating barrier
- Typical junction critical current (Ic): 10-50 nA
- Shunt capacitance: 50-100 fF
- Qubit frequency tunable via external magnetic flux

**Energy Level Structure:**
```
E_n = ℏω_q(n + 1/2) - E_C n² - E_J
where:
  ω_q = qubit frequency
  E_C = charging energy
  E_J = Josephson energy
  n = excitation level
```

**Software Considerations:**
1. **Frequency Collisions**: Must avoid spectral overlap with other qubits or readout resonators
   - Frequency spacing: typically > 100 MHz between nearby qubits
   - Software must track and compensate for frequency drift
   
2. **Anharmonicity**: Energy level spacing decreases for higher levels
   - Typical anharmonicity: α ~ -300 MHz
   - Limits gate fidelity if pulses excite higher levels
   - DRAG pulses compensate for this

3. **Flux Noise**: 1/f noise in flux bias lines causes frequency fluctuations
   - Dephasing time limited to T2* ~ 20-40 μs for flux-tunable qubits
   - Fixed-frequency qubits achieve better T2 times

#### 1.1.2 Coupling Mechanisms

**Fixed Coupling (Capacitive)**
```python
# Typical coupling parameters
g_coupling = 2 * np.pi * 10e6  # 10 MHz coupling strength
qubit_frequencies = [5.0e9, 5.2e9]  # GHz

# Coupling Hamiltonian
H_coupling = g * (a†b + ab†)
# where a, b are annihilation operators for qubits
```

**Tunable Coupling (Coupler Qubits)**
- Intermediate coupler qubit mediates interaction
- Coupling strength adjustable from 0 to ~50 MHz
- Enables selective gate operations
- Software must manage coupler calibration

**Software Implementation:**
```python
class TunableCoupler:
    def __init__(self, coupling_range=(0, 50e6)):
        self.min_coupling = coupling_range[0]
        self.max_coupling = coupling_range[1]
        self.current_coupling = 0
        
    def set_coupling(self, strength):
        """Set coupling strength via flux bias"""
        # Translate to flux bias voltage
        flux_bias = self._strength_to_flux(strength)
        # Send to DAC
        self.dac.set_voltage(flux_bias)
        self.current_coupling = strength
        
    def calibrate_coupling(self, q1, q2):
        """Calibrate coupling via swap oscillations"""
        swap_rates = []
        for strength in np.linspace(0, self.max_coupling, 20):
            self.set_coupling(strength)
            rate = measure_swap_rate(q1, q2)
            swap_rates.append(rate)
        return optimize_coupling_map(swap_rates)
```

#### 1.1.3 Readout Mechanisms

**Dispersive Readout**
- Each qubit coupled to a dedicated resonator
- Qubit state shifts resonator frequency
- Heterodyne measurement of resonator transmission

**Readout Fidelity Factors:**
1. **T1 during measurement** (~300 ns measurement time)
   - Decay during readout reduces fidelity
   - Trade-off: longer measurement = better SNR but more decay

2. **Residual thermal population**
   - P(|1⟩) ~ exp(-ℏω/kT) ≈ 0.5% at 20 mK for 5 GHz qubit
   - Sets fundamental limit on preparation fidelity

3. **Assignment errors**
   - Confusion matrix: P(read 0|state 1) and P(read 1|state 0)
   - Typically 1-3% per qubit
   - Can be mitigated in software

**Software Calibration:**
```python
def calibrate_readout(qubit_id):
    """Measure readout confusion matrix"""
    # Prepare |0⟩ and measure many times
    counts_0 = measure_repeated(qubit_id, state='0', shots=10000)
    p_read0_state0 = counts_0['0'] / 10000
    p_read1_state0 = counts_0['1'] / 10000
    
    # Prepare |1⟩ and measure many times
    counts_1 = measure_repeated(qubit_id, state='1', shots=10000)
    p_read0_state1 = counts_1['0'] / 10000
    p_read1_state1 = counts_1['1'] / 10000
    
    confusion_matrix = np.array([
        [p_read0_state0, p_read1_state0],
        [p_read0_state1, p_read1_state1]
    ])
    
    return confusion_matrix
```

---

### 1.2 Ion Trap Systems - Detailed Analysis

#### 1.2.1 Paul Trap Physics

**RF Trapping Potential:**
```
Φ(r,t) = (U₀ + V₀cos(Ωt))(x² - y²)/(2r₀²) + αz²

where:
  U₀ = DC voltage (endcap)
  V₀ = RF amplitude
  Ω = RF frequency (typically 1-100 MHz)
  r₀ = trap characteristic size
```

**Ion Motion:**
- Secular frequencies: ω_x, ω_y, ω_z (typically 1-10 MHz)
- Micromotion: Fast oscillation at Ω, average <r> = 0
- Software must address secular motion, not micromotion

**Temperature and Cooling:**
```python
def doppler_cooling(ion_species='Yb171'):
    """Implement Doppler cooling sequence"""
    params = {
        'Yb171': {
            'cooling_transition': '369.5 nm',
            'repump_transition': '935 nm',
            'doppler_limit': '0.5 mK'
        }
    }
    
    # Apply red-detuned cooling laser
    laser_detuning = -0.5 * linewidth  # Γ/2
    cooling_time = 1e-3  # 1 ms typical
    
    # Final temperature limited by photon recoil
    T_final = calculate_doppler_limit(ion_species)
    
    return T_final

def sideband_cooling(target_mode='axial'):
    """Ground state cooling via sideband transitions"""
    # Requires narrow-linewidth laser
    # Can reach <n> < 0.1 phonons
    pass
```

#### 1.2.2 Laser Control Systems

**Multi-level Addressing:**
```python
class IonLaserController:
    def __init__(self, num_ions):
        self.num_ions = num_ions
        self.aoms = [AOM(i) for i in range(num_ions)]  # Acousto-optic modulators
        self.beam_positions = self._initialize_beam_positions()
        
    def single_qubit_gate(self, ion_id, gate_type, angle):
        """Apply single-qubit gate to specific ion"""
        # 1. Tune AOM to address specific ion
        self.aoms[ion_id].set_frequency(self.ion_frequencies[ion_id])
        
        # 2. Set pulse parameters
        pulse_duration = angle / rabi_frequency
        pulse_phase = self._compute_phase(gate_type)
        
        # 3. Execute pulse
        self._apply_laser_pulse(
            ion=ion_id,
            duration=pulse_duration,
            phase=pulse_phase,
            detuning=0  # Resonant
        )
        
    def two_qubit_gate(self, control_ion, target_ion):
        """Mølmer-Sørensen gate via phonon mediation"""
        # Use shared vibrational mode
        common_mode_freq = self.motional_frequencies['COM']
        
        # Apply bichromatic light field
        red_detuning = -common_mode_freq
        blue_detuning = +common_mode_freq
        
        # Gate time inversely proportional to coupling strength
        gate_time = np.pi / (2 * coupling_strength)
        
        # Execute pulse sequence
        self._bichromatic_pulse(
            ions=[control_ion, target_ion],
            duration=gate_time,
            red_detuning=red_detuning,
            blue_detuning=blue_detuning
        )
```

**Laser Stabilization:**
- Frequency stability required: < 1 kHz over gate duration
- Techniques:
  1. Cavity locking (Pound-Drever-Hall)
  2. Frequency combs for absolute reference
  3. Feed-forward compensation

**Software Monitoring:**
```python
def monitor_laser_lock():
    """Continuous monitoring of laser frequency lock"""
    while True:
        error_signal = cavity_lock.get_error()
        
        if abs(error_signal) > threshold:
            # Relock laser
            cavity_lock.relock()
            # Recalibrate affected qubits
            recalibrate_affected_ions()
            
        time.sleep(0.1)  # Check every 100 ms
```

#### 1.2.3 Motional Mode Management

**Normal Modes for N ions:**
```python
import numpy as np

def compute_normal_modes(N, trap_frequencies):
    """Calculate normal modes for ion chain"""
    # Build Coulomb interaction matrix
    coulomb_matrix = build_coulomb_matrix(N)
    
    # Add trap potential
    trap_matrix = np.diag([trap_frequencies['x']**2] * N)
    
    # Solve eigenvalue problem
    eigenvalues, eigenvectors = np.linalg.eig(
        trap_matrix + coulomb_matrix
    )
    
    # Sort by frequency
    mode_frequencies = np.sqrt(eigenvalues)
    mode_vectors = eigenvectors
    
    return mode_frequencies, mode_vectors

# For 2 ions in linear trap:
# Center of mass mode: (r₁ + r₂)/√2
# Stretch mode: (r₁ - r₂)/√2
```

**Heating Rate Compensation:**
- Anomalous heating: dn̄/dt ~ 10-100 phonons/s
- Must cool between operations or use motional modes strategically

```python
class MotionalModeManager:
    def __init__(self, ion_chain):
        self.modes = compute_normal_modes(len(ion_chain))
        self.heating_rates = self._measure_heating_rates()
        
    def _measure_heating_rates(self):
        """Measure dn̄/dt for each mode"""
        rates = {}
        for mode in self.modes:
            # Cool to ground state
            sideband_cool(mode)
            
            # Wait varying times and measure phonon number
            wait_times = np.linspace(0, 10e-3, 10)
            phonon_numbers = []
            
            for t in wait_times:
                wait(t)
                n_bar = measure_phonon_number(mode)
                phonon_numbers.append(n_bar)
            
            # Fit linear slope
            rates[mode] = np.polyfit(wait_times, phonon_numbers, 1)[0]
            
        return rates
    
    def optimize_gate_mode(self, gate_type):
        """Select optimal motional mode for gate"""
        if gate_type == 'MS':  # Mølmer-Sørensen
            # Prefer mode with:
            # 1. Low heating rate
            # 2. Good coupling to both ions
            # 3. Well-separated from other modes
            
            scores = []
            for mode in self.modes:
                score = (
                    1 / self.heating_rates[mode] *
                    coupling_strength(mode) *
                    frequency_separation(mode)
                )
                scores.append(score)
            
            return self.modes[np.argmax(scores)]
```

---

### 1.3 Photonic Quantum Computing

#### 1.3.1 Single Photon Sources

**Spontaneous Parametric Down-Conversion (SPDC):**
```python
class SPDCSource:
    def __init__(self, crystal_type='BBO'):
        self.crystal = crystal_type
        self.pump_wavelength = 405e-9  # nm (blue)
        self.signal_wavelength = 810e-9  # nm (infrared)
        self.generation_rate = 1e6  # photons/s
        
    def generate_photon_pair(self):
        """Generate entangled photon pair"""
        # Phase matching condition determines wavelengths
        # Conservation of energy: ω_pump = ω_signal + ω_idler
        # Conservation of momentum: k_pump = k_signal + k_idler
        
        # Probabilistic generation
        if random.random() < self.generation_efficiency:
            return PhotonPair(
                wavelengths=[self.signal_wavelength, self.signal_wavelength],
                polarization_entangled=True
            )
        return None
```

**Quantum Dot Single Photon Sources:**
- Deterministic generation on demand
- InGaAs quantum dots in cavities
- Challenges: Indistinguishability, timing jitter

**Software Challenges:**
```python
def heralded_photon_source():
    """Use SPDC with heralding for quasi-deterministic source"""
    while True:
        pair = spdc_source.generate()
        if pair:
            # Detect idler photon
            if detector_idler.clicked():
                # Signal photon heralded
                return pair.signal_photon
            else:
                # Lost photon pair
                continue
        # Waiting for next pair
        time.sleep(clock_period)
```

#### 1.3.2 Linear Optical Gates

**Beam Splitter Operations:**
```python
def beam_splitter_transformation(r, t):
    """
    Beam splitter unitary matrix
    r: reflection coefficient
    t: transmission coefficient
    |r|² + |t|² = 1 (energy conservation)
    """
    return np.array([
        [t, r],
        [r, -t]
    ])

# 50:50 beam splitter
BS_5050 = beam_splitter_transformation(1/np.sqrt(2), 1/np.sqrt(2))

def hong_ou_mandel_interference():
    """Demonstrate HOM interference - foundation of photonic QC"""
    # Two identical photons entering different ports of BS
    # Outcome: Always both exit same port (bunching)
    
    initial_state = [1, 1]  # One photon in each input
    # After BS: only |2,0⟩ and |0,2⟩, never |1,1⟩
    
    # Visibility measures indistinguishability
    visibility = measure_hom_dip()
    return visibility  # Should approach 1.0 for identical photons
```

**CNOT Gate via KLM Protocol:**
```python
def linear_optical_cnot(control, target):
    """
    CNOT using Knill-Laflamme-Milburn protocol
    Requires ancilla photons and post-selection
    """
    # Non-deterministic: succeeds with probability ~ 1/16
    
    # Use beam splitters and phase shifters
    ancilla1 = single_photon_source.generate()
    ancilla2 = single_photon_source.generate()
    
    # Complex interferometer network
    circuit = [
        beam_splitter(control, ancilla1),
        phase_shift(ancilla1, np.pi/2),
        beam_splitter(ancilla1, target),
        beam_splitter(control, ancilla2),
        # ... more operations
    ]
    
    # Measure ancillas
    m1 = measure(ancilla1)
    m2 = measure(ancilla2)
    
    # Post-select on specific outcomes
    if (m1, m2) == (0, 0):
        return True  # Success
    else:
        return False  # Retry needed
```

#### 1.3.3 Measurement-Based Quantum Computing

**Cluster State Generation:**
```python
def generate_cluster_state(lattice_size):
    """
    Create 2D cluster state for MBQC
    Lattice of qubits with CZ gates between neighbors
    """
    N_rows, N_cols = lattice_size
    
    # Initialize all qubits in |+⟩
    state = [hadamard_state() for _ in range(N_rows * N_cols)]
    
    # Apply CZ between nearest neighbors
    for i in range(N_rows):
        for j in range(N_cols):
            current = i * N_cols + j
            
            # Right neighbor
            if j < N_cols - 1:
                apply_cz(current, current + 1)
            
            # Bottom neighbor
            if i < N_rows - 1:
                apply_cz(current, current + N_cols)
    
    return state

def mbqc_computation(cluster, measurement_pattern):
    """
    Execute computation via adaptive measurements
    """
    results = []
    
    for qubit_id, basis_angle in measurement_pattern:
        # Measurement basis depends on previous results
        adapted_angle = adapt_measurement_basis(
            basis_angle, 
            previous_results=results
        )
        
        # Measure in rotated basis
        result = measure_in_basis(
            cluster[qubit_id], 
            angle=adapted_angle
        )
        results.append(result)
    
    # Final result encoded in measurement pattern
    return decode_output(results)
```

---

### 1.4 Neutral Atom Platforms

#### 1.4.1 Optical Tweezer Arrays

**Tweezer Generation:**
```python
class OpticalTweezerArray:
    def __init__(self, num_tweezers):
        self.slm = SpatialLightModulator()  # Phase modulation
        self.objective = Objective(NA=0.5)  # High NA lens
        self.trap_depth = 1e-3  # 1 mK
        
    def create_arbitrary_array(self, positions):
        """
        Generate arbitrary 2D array of traps
        positions: list of (x, y) coordinates in μm
        """
        # Compute hologram using Gerchberg-Saxton algorithm
        hologram = self.compute_hologram(positions)
        
        # Load onto SLM
        self.slm.display_pattern(hologram)
        
        # Focus through objective creates trap array
        return self.trap_array
    
    def rearrange_atoms(self, initial_pos, target_pos):
        """
        Move atoms between configurations
        Useful for creating optimal gate connectivity
        """
        # Plan collision-free trajectory
        trajectories = plan_rearrangement(initial_pos, target_pos)
        
        # Execute move (typically < 100 ms)
        for step in trajectories:
            self.update_tweezer_positions(step)
            time.sleep(0.001)  # 1 ms steps
```

**Atom Loading:**
```python
def stochastic_loading_sequence():
    """
    Load atoms from MOT into tweezers
    Poissonian statistics: mean loading ~ 0.5 atoms/trap
    """
    # Cool atoms in MOT
    mot_temperature = 100e-6  # 100 μK
    
    # Turn on tweezers
    tweezers.activate()
    
    # Wait for atoms to be captured
    time.sleep(0.1)  # 100 ms
    
    # Detect which traps filled
    occupancy = []
    for trap in tweezers:
        fluorescence = detect_fluorescence(trap)
        if fluorescence > threshold:
            occupancy.append(1)
        else:
            occupancy.append(0)
    
    return occupancy

def deterministic_filling(target_array):
    """
    Achieve deterministic filling via rearrangement
    """
    # Load with redundancy
    loaded = stochastic_loading_sequence()
    filled_sites = [i for i, occ in enumerate(loaded) if occ == 1]
    
    # Move filled traps to target positions
    if len(filled_sites) >= len(target_array):
        # Rearrange filled traps to target
        tweezers.rearrange_atoms(filled_sites[:len(target_array)], target_array)
        return True
    else:
        # Not enough atoms, reload
        return False
```

#### 1.4.2 Rydberg Blockade Mechanism

**Physics:**
- Excite atoms to high-lying Rydberg states (n ~ 50-100)
- Strong van der Waals interaction: V(r) = C₆/r⁶
- Blockade radius: r_b ≈ (C₆/ℏΩ)^(1/6)

**Software Implementation:**
```python
class RydbergBlockadeGate:
    def __init__(self, rydberg_state='60S'):
        self.principal_n = 60
        self.C6_coefficient = self._compute_C6()
        self.rabi_frequency = 2 * np.pi * 1e6  # 1 MHz
        
    def _compute_C6(self):
        """Van der Waals coefficient for given Rydberg state"""
        # Scales approximately as n^11
        return 5e6 * (self.principal_n / 60)**11  # GHz·μm⁶
    
    def blockade_radius(self):
        """Compute blockade radius"""
        r_b = (self.C6_coefficient / self.rabi_frequency)**(1/6)
        return r_b  # in μm
    
    def cz_gate(self, atom1, atom2):
        """
        Controlled-Z gate via blockade
        """
        distance = compute_distance(atom1, atom2)
        
        # Check blockade condition
        if distance < self.blockade_radius():
            # Apply Rydberg π pulse to control
            # If control in |1⟩, target blocked
            
            pulse_sequence = [
                ('Rydberg_pi', [atom1]),
                ('Rydberg_2pi', [atom2]),  # Blocked if atom1 excited
                ('Rydberg_pi', [atom1])
            ]
            
            execute_pulse_sequence(pulse_sequence)
            return True
        else:
            raise ValueError("Atoms too far for blockade")
    
    def global_rydberg_gate(self, atom_list):
        """
        Apply same Rydberg pulse to many atoms
        Enables parallel gate operations
        """
        # All atoms illuminated by same laser
        global_rydberg_pulse(
            atoms=atom_list,
            pulse_area=np.pi,  # π pulse
            detuning=0
        )
```

#### 1.4.3 Analog Quantum Simulation

**Ising Hamiltonian Simulation:**
```python
def program_ising_hamiltonian(atom_array, parameters):
    """
    Implement Ising model H = Σ Ω/2 σᵢˣ - Σ δ/2 σᵢᶻ + Σ V_ij σᵢᶻσⱼᶻ
    
    atom_array: 2D positions of atoms
    parameters: {Omega, delta, evolution_time}
    """
    # Rabi frequency Ω (global)
    global_rabi = parameters['Omega']
    
    # Detuning δ (can be site-dependent)
    detunings = parameters['delta']
    
    # Interaction V_ij determined by atomic positions
    # V_ij = C6 / |r_i - r_j|^6
    
    # Time evolution
    t_evolve = parameters['evolution_time']
    
    # Program pulse sequence
    pulse_program = {
        'duration': t_evolve,
        'global_rabi': global_rabi,
        'detunings': detunings
    }
    
    # Execute
    execute_analog_program(pulse_program)
    
    # Measure in computational basis
    results = measure_all_atoms()
    
    return results

# Example: Find ground state of Ising model (optimization)
def quantum_annealing_sweep():
    """Adiabatic evolution to find ground state"""
    T_anneal = 1e-3  # 1 ms
    steps = 100
    
    for i in range(steps):
        # Sweep from paramagnetic to antiferromagnetic
        Omega = Omega_max * (1 - i/steps)
        delta = delta_max * (i/steps)
        
        program_ising_hamiltonian(
            atom_array=current_array,
            parameters={
                'Omega': Omega,
                'delta': delta,
                'evolution_time': T_anneal/steps
            }
        )
    
    # Final measurement gives (approximate) ground state
    ground_state = measure_all_atoms()
    energy = compute_energy(ground_state)
    
    return ground_state, energy
```

---

## Section 2: Quantum Software Stack - Deep Dive

### 2.1 Control Layer Implementation

#### 2.1.1 Pulse Shaping Mathematics

**Gaussian Pulse:**
```python
def gaussian_pulse(t, amplitude, center, sigma):
    """
    g(t) = A · exp[-(t - t₀)²/(2σ²)]
    
    Fourier transform approximately Gaussian in frequency
    Width in time: Δt ~ σ
    Width in frequency: Δf ~ 1/(2πσ)
    """
    return amplitude * np.exp(-((t - center)**2) / (2 * sigma**2))

# Spectral leakage
def pulse_spectrum(pulse_func, sample_rate=1e9):
    """Compute frequency spectrum of pulse"""
    time_points = np.linspace(0, 1e-6, int(sample_rate * 1e-6))
    pulse_samples = pulse_func(time_points)
    
    spectrum = np.fft.fft(pulse_samples)
    frequencies = np.fft.fftfreq(len(time_points), 1/sample_rate)
    
    return frequencies, np.abs(spectrum)
```

**DRAG Pulse (Derivative Removal by Adiabatic Gate):**
```python
def drag_pulse(t, amplitude, sigma, alpha=-0.5):
    """
    Quadrature components:
    I(t) = A · g(t)
    Q(t) = α · A · g'(t)
    
    where g'(t) is derivative of Gaussian
    α typically -0.3 to -0.5
    """
    gaussian = np.exp(-(t**2) / (2 * sigma**2))
    gaussian_derivative = -(t / sigma**2) * gaussian
    
    I_component = amplitude * gaussian
    Q_component = alpha * amplitude * gaussian_derivative
    
    return I_component + 1j * Q_component

# Why DRAG works: Cancels AC Stark shift from pulse envelope
# Reduces leakage to |2⟩ state in transmon
```

**Optimal Control Theory:**
```python
from scipy.optimize import minimize

def grape_optimization(target_unitary, initial_pulse, num_segments=100):
    """
    GRAPE: Gradient Ascent Pulse Engineering
    Optimize pulse to achieve target unitary
    """
    def fidelity_function(pulse_params):
        # Simulate time evolution with pulse
        U_achieved = simulate_unitary(
            pulse=construct_pulse(pulse_params),
            num_segments=num_segments
        )
        
        # Fidelity with target
        fidelity = np.abs(np.trace(U_achieved.conj().T @ target_unitary))**2
        fidelity /= target_unitary.shape[0]**2
        
        return -fidelity  # Minimize negative fidelity
    
    # Optimize
    result = minimize(
        fidelity_function,
        x0=initial_pulse,
        method='BFGS',
        options={'maxiter': 1000}
    )
    
    optimal_pulse = construct_pulse(result.x)
    final_fidelity = -result.fun
    
    return optimal_pulse, final_fidelity
```

#### 2.1.2 Cross-Talk Mitigation

**Sources of Cross-Talk:**
1. Flux cross-talk: Flux bias on one qubit affects neighbors
2. Readout cross-talk: Photons leak between resonators
3. Parasitic coupling: Unintended capacitive coupling
4. Control line cross-talk: Signal bleed through wiring

**Mitigation Strategies:**
```python
class CrossTalkCompensator:
    def __init__(self, num_qubits):
        self.num_qubits = num_qubits
        self.crosstalk_matrix = None
        
    def calibrate_crosstalk(self):
        """Measure crosstalk between all qubit pairs"""
        matrix = np.zeros((self.num_qubits, self.num_qubits))
        
        for i in range(self.num_qubits):
            for j in range(self.num_qubits):
                if i != j:
                    # Apply pulse to qubit i
                    # Measure effect on qubit j
                    crosstalk = measure_frequency_shift(
                        target=i,
                        victim=j
                    )
                    matrix[i, j] = crosstalk
        
        self.crosstalk_matrix = matrix
        return matrix
    
    def compensate_pulse(self, target_qubit, pulse):
        """
        Pre-distort pulse to cancel cross-talk
        """
        # Invert cross-talk matrix
        compensation_matrix = np.linalg.inv(
            np.eye(self.num_qubits) + self.crosstalk_matrix
        )
        
        # Apply compensation
        all_pulses = np.zeros((self.num_qubits, len(pulse)))
        all_pulses[target_qubit] = pulse
        
        compensated = compensation_matrix @ all_pulses
        
        return compensated

# Echo-based cross-talk suppression
def cross_talk_echo_sequence(gate_sequence):
    """
    Insert echo pulses to cancel unwanted ZZ coupling
    """
    echoed_sequence = []
    
    for gate in gate_sequence:
        echoed_sequence.append(gate)
        
        # Add compensating pulse
        if is_two_qubit_gate(gate):
            # Insert X gates on idle qubits during gate
            idle_qubits = get_idle_qubits(gate)
            for q in idle_qubits:
                echoed_sequence.append(('X', q))
                echoed_sequence.append(('X', q))  # Net identity
    
    return echoed_sequence
```

---

### 2.2 Middleware Layer - Advanced Topics

#### 2.2.1 Circuit Optimization Algorithms

**Template Matching:**
```python
def template_substitution(circuit):
    """
    Replace subcircuits with optimized equivalents
    """
    templates = {
        # CNOT cancellation
        ('CNOT', 'CNOT'): Identity(),
        
        # Hadamard cancellation
        ('H', 'H'): Identity(),
        
        # Rotation combining
        ('RZ(θ₁)', 'RZ(θ₂)'): lambda theta1, theta2: RZ(theta1 + theta2),
        
        # CNOT reduction: H-CNOT-H = CNOT with swapped control/target
        ('H', 'CNOT', 'H'): lambda control, target: CNOT(target, control)
    }
    
    optimized = circuit.copy()
    
    # Scan for matching patterns
    for pattern, replacement in templates.items():
        optimized = find_and_replace(optimized, pattern, replacement)
    
    return optimized

# Peephole optimization
def peephole_optimize(circuit, window_size=3):
    """
    Local optimization over sliding window
    """
    for i in range(len(circuit) - window_size):
        window = circuit[i:i+window_size]
        
        # Try all possible reorderings
        best_window = window
        min_cost = cost_function(window)
        
        for permutation in all_valid_reorderings(window):
            if commutes(permutation):
                current_cost = cost_function(permutation)
                if current_cost < min_cost:
                    best_window = permutation
                    min_cost = current_cost
        
        circuit[i:i+window_size] = best_window
    
    return circuit
```

**Commutation Analysis:**
```python
def commutation_dag(circuit):
    """
    Build directed acyclic graph of gate dependencies
    Gates commute if they act on disjoint qubits
    """
    dag = nx.DiGraph()
    
    for gate_id, gate in enumerate(circuit):
        dag.add_node(gate_id, gate=gate)
        
        # Add edges to previous gates on same qubits
        affected_qubits = gate.qubits
        
        for prev_id in range(gate_id):
            prev_gate = circuit[prev_id]
            
            # Check qubit overlap
            if set(affected_qubits) & set(prev_gate.qubits):
                dag.add_edge(prev_id, gate_id)
    
    return dag

def maximize_parallelism(circuit):
    """
    Schedule gates to minimize circuit depth
    """
    dag = commutation_dag(circuit)
    
    # Topological sort with longest path
    levels = nx.dag_longest_path_length(dag)
    
    schedule = [[] for _ in range(levels)]
    
    for node in nx.topological_sort(dag):
        # Find earliest level where gate can execute
        predecessors = list(dag.predecessors(node))
        
        if not predecessors:
            earliest_level = 0
        else:
            earliest_level = max(schedule_level[p] for p in predecessors) + 1
        
        schedule[earliest_level].append(node)
    
    return schedule
```

#### 2.2.2 Qubit Routing Algorithms

**SABRE Algorithm (SWAP-based bidirectional heuristic):**
```python
class SABRERouter:
    def __init__(self, coupling_map, lookahead_depth=20):
        self.coupling_map = coupling_map
        self.lookahead = lookahead_depth
        
    def route_circuit(self, logical_circuit):
        """
        Route circuit onto hardware topology using SWAP insertion
        """
        # Initialize mapping
        current_mapping = self._initial_mapping(logical_circuit)
        routed_circuit = []
        
        # Front layer: gates ready to execute
        front_layer = self._get_executable_gates(logical_circuit, current_mapping)
        
        while logical_circuit or front_layer:
            # Execute all gates in front layer that respect topology
            executed = []
            for gate in front_layer:
                if self._is_executable(gate, current_mapping):
                    physical_gate = self._map_to_physical(gate, current_mapping)
                    routed_circuit.append(physical_gate)
                    executed.append(gate)
            
            # Remove executed gates
            for gate in executed:
                front_layer.remove(gate)
                logical_circuit.remove(gate)
            
            # Update front layer
            front_layer.extend(self._get_executable_gates(logical_circuit, current_mapping))
            
            # If front layer blocked, insert SWAPs
            if front_layer and not any(self._is_executable(g, current_mapping) for g in front_layer):
                swap = self._choose_best_swap(front_layer, current_mapping)
                routed_circuit.append(swap)
                current_mapping = self._apply_swap(current_mapping, swap)
        
        return routed_circuit
    
    def _choose_best_swap(self, front_layer, mapping):
        """
        Heuristic: minimize distance between logical qubits
        """
        scores = {}
        
        for potential_swap in self._candidate_swaps(mapping):
            # Score based on reducing distance for front layer gates
            score = 0
            temp_mapping = self._apply_swap(mapping, potential_swap)
            
            # Immediate improvement
            for gate in front_layer[:self.lookahead]:
                if self._is_executable(gate, temp_mapping):
                    score += 10  # Immediate execution is valuable
                else:
                    # Penalize by distance
                    dist = self._gate_distance(gate, temp_mapping)
                    score -= dist
            
            scores[potential_swap] = score
        
        # Return best SWAP
        best_swap = max(scores, key=scores.get)
        return best_swap
```

**Layout Optimization:**
```python
def optimal_initial_layout(circuit, coupling_map):
    """
    Find good initial mapping of logical to physical qubits
    Minimize expected number of SWAPs
    """
    # Build interaction graph from circuit
    interaction_graph = nx.Graph()
    
    for gate in circuit:
        if len(gate.qubits) == 2:
            q1, q2 = gate.qubits
            if interaction_graph.has_edge(q1, q2):
                interaction_graph[q1][q2]['weight'] += 1
            else:
                interaction_graph.add_edge(q1, q2, weight=1)
    
    # Find subgraph isomorphism that preserves high-weight edges
    # This is NP-hard, use heuristic
    
    best_mapping = None
    best_score = float('inf')
    
    for trial in range(100):  # Try 100 random layouts
        mapping = random_mapping(circuit.num_qubits, coupling_map.num_qubits)
        
        score = evaluate_mapping(mapping, interaction_graph, coupling_map)
        
        if score < best_score:
            best_score = score
            best_mapping = mapping
    
    return best_mapping

def evaluate_mapping(mapping, interaction_graph, coupling_map):
    """Score based on distance between interacting qubits"""
    score = 0
    
    for logical_q1, logical_q2 in interaction_graph.edges():
        physical_q1 = mapping[logical_q1]
        physical_q2 = mapping[logical_q2]
        
        # Distance in coupling graph
        distance = nx.shortest_path_length(
            coupling_map.graph,
            physical_q1,
            physical_q2
        )
        
        # Weight by interaction frequency
        weight = interaction_graph[logical_q1][logical_q2]['weight']
        
        score += distance * weight
    
    return score
```

