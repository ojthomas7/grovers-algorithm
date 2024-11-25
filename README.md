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

We then construct our oracle which creates a phase flip for our target state but not the others. The oracle acts on a state such that:

$$|x\rangle|q\rangle \to |x\rangle|q \oplus \rangle f(x)$$

Where $|x\rangle$ is the index register and $|q\rangle$ is a single qubit whichh is flipped if $f(x) = 1$ and unchanged otherwise.


In this algorithm, we apply the oracle to the state $|-\rangle = \frac{1}{\sqrt{2}}(|0\rangle - |1\rangle)$. This is helpful, as if we have the case where $|x\rangle$ is the solution to the search problem, the states $|0\rangle$ and $|1\rangle$ are interchanged by the oracle, and are unchanged if not.

The action of the oracle is therefore:

$$|x\rangle(\frac{1}{\sqrt{2}}(|0\rangle - |1\rangle)) \to (-1)^{f(x)}|x\rangle (\frac{1}{\sqrt{2}}(|0\rangle - |1\rangle))$$


The $|-\rangle$ state is then omitted as it appears throughout the search algorithm fo simplification:

$$|x\rangle\to (-1)^{f(x)}|x\rangle$$

## The Procedure

In this example, building a circuit demonstrating Grovers algorithm in Qiskit, we start by building a simple oracle which applies a phase flip when acted upon the state $|11\rangle$:

```python
oracle = QuantumCircuit(2, name='oracle')
oracle.cz(0,1)
oracle.to_gate()
oracle.draw()
```
