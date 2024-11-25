# Quantum Search: Grovers Algorithm

Suppose we want to search through a set of data, and want to locate the position of a particular value. On a classical computer, if there are $N$ values, then it would require $O(N)$ operations to find the index of the value we are searcing for. Using a quantum algorithm known as Grovers algorithm we can speed this up, requiring $O(\sqrt{N})$ operations.

This implementation demonstrates Grover's algorithm using Qiskit to search for specific values in an unordered list.

## Overview

The circuit searches an unordered list using a 2 qubit quantum system to encode and find target values. We use a 2 qubit system for simplicty in our example, however this can be extended to work in a more general case for more qubits.

## Implementing the Algorithm

### Initialisation

Using the Qiskit SDK we create our 2 qubit system. In this example we are searching through the list to locate the target value 3, however this target can be changed, seen in the construction of the Oracle.

```python
search_list = [3, 0, 1, 2]
target_value = 2
```
 The values are then converted to binary for input to the circuit, bearing in mind the order in which Qiskit reads binary inputs.

 
### The Oracle

We then construct our oracle which creates a phase flip for our target state but not the others:

```python
oracle = QuantumCircuit(2, name='oracle')

if target_binary == '11':
    oracle.cz(0, 1)
elif target_binary == '01':
    oracle.x(1)
    oracle.cz(0, 1)
    oracle.x(1)
elif target_binary == '10':
    oracle.x(0)
    oracle.cz(0, 1)
    oracle.x(0)
elif target_binary == '00':
    oracle.x([0, 1])
    oracle.cz(0, 1)
    oracle.x([0, 1])
oracle_gate = oracle.to_gate()

oracle.draw()
```


## The Procedure

In this example, building a circuit demonstrating Grovers algorithm in Qiskit, we start by building a simple oracle which applies a phase flip when acted upon the state $|11\rangle$:

```python
oracle = QuantumCircuit(2, name='oracle')
oracle.cz(0,1)
oracle.to_gate()
oracle.draw()
```
