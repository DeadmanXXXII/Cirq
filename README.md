# Cirq


### **Cirq CLI Overview**

Cirq is a Python library for designing, simulating, and running quantum circuits on quantum computers. Although it is primarily used through Python scripts.

### **1. Cirq Installation**

Ensure you have Cirq installed:
```bash
pip install cirq
```

### **2. General Cirq CLI Commands**

Cirq does not have a dedicated CLI like Qiskit but relies on Python scripts to interact with quantum circuits and devices. Below are some common tasks you might perform with Cirq using Python scripts executed from the command line.

### **3. Running Cirq Scripts**

Create a Python script (`my_circuit.py`) that uses Cirq:
```python
import cirq

# Create a qubit
qubit = cirq.GridQubit(0, 0)

# Create a circuit
circuit = cirq.Circuit(
    cirq.X(qubit)**0.5,  # Square root of X gate
    cirq.measure(qubit, key='m')  # Measurement
)

# Simulate the circuit
simulator = cirq.Simulator()
result = simulator.run(circuit, repetitions=10)
print(result)
```

Run the script from the command line:
```bash
python my_circuit.py
```

### **4. Cirq Simulation and Execution**

- **Simulate a quantum circuit:**
  ```python
  import cirq

  # Create qubits
  qubits = [cirq.GridQubit(0, i) for i in range(2)]

  # Create a circuit
  circuit = cirq.Circuit(
      cirq.H(qubits[0]),  # Hadamard gate
      cirq.CNOT(qubits[0], qubits[1]),  # CNOT gate
      cirq.measure(*qubits, key='result')  # Measurement
  )

  # Simulate the circuit
  simulator = cirq.Simulator()
  result = simulator.run(circuit, repetitions=10)
  print(result)
  ```

Run the simulation script:
```bash
python simulate_circuit.py
```

### **5. Advanced Execution and Simulation Options**

- **Run a circuit with noise model:**
  ```python
  import cirq
  import cirq.google as cg

  # Create qubits
  qubits = [cirq.GridQubit(0, i) for i in range(2)]

  # Create a circuit
  circuit = cirq.Circuit(
      cirq.H(qubits[0]),
      cirq.CNOT(qubits[0], qubits[1]),
      cirq.measure(*qubits, key='result')
  )

  # Create a noise model
  noise_model = cg.PhasedFSimEngineSimulator.create_noise_model_from_calibration_data(cg.engine, 'processor_id', 'gate_set')
  
  # Simulate the circuit with noise
  noisy_simulator = cirq.DensityMatrixSimulator(noise=noise_model)
  result = noisy_simulator.run(circuit, repetitions=10)
  print(result)
  ```

### **6. Managing and Listing Devices**

- **List Google devices:**
  ```python
  import cirq.google as cg

  # List available processors
  engine = cg.Engine(project_id='your_project_id')
  print(engine.list_processors())
  ```

- **Get details of a specific device:**
  ```python
  processor = engine.get_processor('your_processor_id')
  print(processor)
  ```

### **7. Cirq Optimizations and Transformations**

- **Optimize a circuit:**
  ```python
  import cirq

  # Create a circuit
  qubit = cirq.GridQubit(0, 0)
  circuit = cirq.Circuit(cirq.X(qubit)**0.5, cirq.X(qubit)**0.5)

  # Optimize the circuit
  optimized_circuit = cirq.optimize_for_sycamore(circuit)
  print(optimized_circuit)
  ```

- **Transform a circuit:**
  ```python
  import cirq

  # Create a circuit
  qubit = cirq.GridQubit(0, 0)
  circuit = cirq.Circuit(cirq.X(qubit)**0.5, cirq.Y(qubit)**0.5)

  # Transform the circuit
  transformed_circuit = cirq.merge_single_qubit_gates_to_phxz(circuit)
  print(transformed_circuit)
  ```

### **8. Using Cirq with Google Quantum Engine**

- **Run a circuit on a Google Quantum Processor:**
  ```python
  import cirq
  import cirq.google as cg

  # Create a circuit
  qubit = cirq.GridQubit(0, 0)
  circuit = cirq.Circuit(cirq.X(qubit)**0.5, cirq.measure(qubit, key='m'))

  # Set up the engine
  engine = cg.Engine(project_id='your_project_id')

  # Run the circuit
  result = engine.run(circuit=circuit, processor_ids=['your_processor_id'], repetitions=10)
  print(result)
  ```

### **9. Miscellaneous Commands**

- **Export circuit to QASM:**
  ```python
  import cirq

  # Create a circuit
  qubit = cirq.GridQubit(0, 0)
  circuit = cirq.Circuit(cirq.X(qubit)**0.5, cirq.measure(qubit, key='m'))

  # Export to QASM
  qasm_output = cirq.qasm(circuit)
  print(qasm_output)
  ```

- **Import circuit from QASM:**
  ```python
  import cirq

  # QASM input
  qasm_input = """
  OPENQASM 2.0;
  include "qelib1.inc";
  qreg q[1];
  creg c[1];
  x q[0];
  measure q[0] -> c[0];
  """

  # Import from QASM
  circuit = cirq.circuits.qasm_import.qasm_to_circuit(qasm_input)
  print(circuit)
  ```

### **10. Working with Cirq from Jupyter Notebooks**

You can also run Cirq commands in Jupyter Notebooks for interactive development and visualization.

- **Install Jupyter Notebook:**
  ```bash
  pip install notebook
  ```

- **Start Jupyter Notebook:**
  ```bash
  jupyter notebook
  ```

- **Run Cirq in a notebook cell:**
  ```python
  import cirq

  # Create a qubit
  qubit = cirq.GridQubit(0, 0)

  # Create a circuit
  circuit = cirq.Circuit(
      cirq.X(qubit)**0.5,
      cirq.measure(qubit, key='m')
  )

  # Simulate the circuit
  simulator = cirq.Simulator()
  result = simulator.run(circuit, repetitions=10)
  print(result)
  ```

### **Conclusion**

This comprehensive list covers a wide range of Cirq CLI commands and Python script examples for managing and simulating quantum circuits. It includes basic operations, advanced execution options, device management, and optimizations, providing a thorough guide for interacting with Cirq from the command line.
