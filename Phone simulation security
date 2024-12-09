from qiskit import QuantumCircuit, transpile, assemble
from qiskit_aer import AerSimulator
from qiskit.visualization import plot_histogram
import numpy as np
import matplotlib.pyplot as plt

# Create a Quantum Circuit with 2 qubits and 4 classical bits
qc = QuantumCircuit(2, 4)

# Apply Hadamard gate on both qubits to create superposition
qc.h([0, 1])

# Apply CNOT gate to entangle the qubits
qc.cx(0, 1)

# Simulate an eavesdropper by measuring qubit 0
qc.measure(0, 0)

# Apply additional gates to simulate a response to detection
qc.h(1)
qc.cx(1, 0)

# Measure all qubits
qc.measure([0, 1], [1, 2])

# Draw the circuit
qc.draw('mpl')
plt.show()

# Use AerSimulator
simulator = AerSimulator()

# Transpile the circuit for the simulator
compiled_circuit = transpile(qc, simulator)

# Assemble the circuit into a Qobj
qobj = assemble(compiled_circuit)

# Execute the circuit on the Aer simulator
result = simulator.run(qobj).result()

# Get the counts (measurement results)
counts = result.get_counts(qc)
print("Measurement Results:", counts)

# Plot the results
plot_histogram(counts)
plt.show()

# Calculate entropy
def calculate_entropy(counts):
    total_shots = sum(counts.values())
    entropy = 0
    for count in counts.values():
        probability = count / total_shots
        entropy -= probability * np.log2(probability)
    return entropy

entropy_value = calculate_entropy(counts)
print(f"Entropy: {entropy_value}")

# Simulate a response based on entropy
if entropy_value > 1.0:
    print("Unauthorized access detected. Taking action.")
else:
    print("System secure.")
