# Quantum Search: Grovers Algorithm

Suppose we want to search through a set of data, and want to locate the position of a particular value. On a classical computer, if there are $N$ values, then it would require $O(N)$ operations to find the index of the value we are searcing for. Using a quantum algorithm known as Grovers algorithm we can speed this up, requiring $O(\sqrt{N})$ operations.

## The Oracle

We use a quanutm oracle: a blakcbox with the baility to recognise the solution to the search problem. The oracle acts on a state such that:

$$|x\rangle|q\rangle \to |x\rangle|q \oplus \rangle f(x)$$

Where $|x\rangle$ is the index register and $|q\rangle$ is a single qubit whichh is flipped if $f(x) = 1$ and unchanged otherwise.


In this algorithm, we apply the oracle to the state $|-\rangle = \frac{1}{\sqrt{2}}(|0\rangle - |1\rangle)$. This is helpful, as if we have the case where $|x\rangle$ is the solution to the search problem, the states $|0\rangle$ and $|1\rangle$ are interchanged by the oracle, and are unchanged if not.

The action of the oracle is therefore:

$$|x\rangle(\frac{1}{\sqrt{2}}(|0\rangle - |1\rangle)) \to (-1)^{f(x)}|x\rangle (\frac{1}{\sqrt{2}}(|0\rangle - |1\rangle))$$


The $|-\rangle$ state is then omitted as it appears throughout the search algorithm fo simplification:

$$|x\rangle\to (-1)^{f(x)}|x\rangle$$
