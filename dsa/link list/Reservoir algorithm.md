Algorithm R randomly selects k elements from a stream of n elements, where n is an unknown large number. The algorithm has a fixed memory that can store only k elements at a time. Initially, the memory is empty.

The proof by mathematical induction shows that if Algorithm R has already selected k elements from the stream, and the probability of any particular element being included in the k elements is k/i, where i is the number of elements seen so far, then the probability of the next element being included in the k elements is (k/(i+1)).

To prove this, we assume that the induction hypothesis is true for i, i.e., the probability of any particular element being included in the k elements is k/i. Now, we show that the probability of the next element being included in the k elements is (k/(i+1)).

When the (i+1)th element is seen, it is included in the memory with a probability of k/(i+1) (as given in the algorithm). For any other element j (where k+1 <= j <= i+1), the probability that it was included in the memory before the (i+1)th element is seen is k/i (by the induction hypothesis).

Now, we need to find the probability that the element j remains in the memory even after the (i+1)th element is seen. The probability of j not being replaced by the (i+1)th element is given by the product of two probabilities: (i) the probability that j was in the memory before the (i+1)th element was seen (k/i), and (ii) the probability that j is not replaced by the (i+1)th element (1 - 1/(i+1)).

We can simplify this to get the probability that j is still in the memory after the (i+1)th element is seen, which is (k/i) * (1 - 1/(i+1)) = (k/(i+1)).

Therefore, the probability of any particular element being included in the k elements after the (i+1)th element is seen is (k/(i+1)). This completes the proof by mathematical induction.

In summary, the proof shows that Algorithm R randomly selects k elements from a stream of n elements with a probability of k/n for each element, without knowing the value of n in advance.

- wiki link - [[Reservoir sampling - Wikipedia](https://en.wikipedia.org/wiki/Reservoir_sampling)]