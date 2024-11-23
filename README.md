# Quantum Search: Grovers Algorithm

Suppose we want to search through a set of data, and want to locate the position of a particular value. On a classical computer, if there are $N$ values, then it would require $O(N)$ operations to find the index of the value we are searcing for. Using a quantum algorithm known as Grovers algorithm we can speed this up, requiring $O(\sqrt{N})$ operations.

## The Oracle

We use a quanutm oracle: a blakcbox with the baility to recognise the solution to the search problem. The oracle acts on a state such that:

$$|x\rangle|q\rangle \to |x\rangle|q \oplus \rangle$$
