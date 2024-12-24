> ### Q
> 1. What is the definition of epsilon-delta?
> 2. Can you prove the epsilon-delta theorem?

> ### A
> 애슬론 델타 정의와 증명  
> 2m 27s 동안 생각

**1. What is the epsilon-delta definition?**

The epsilon-delta definition is a formal way to define the limit of a function at a certain point. Specifically, consider a function \( f: \mathbb{R} \to \mathbb{R} \) and a point \( a \in \mathbb{R} \). We say that the limit of \( f(x) \) as \( x \) approaches \( a \) is \( L \), and write

\[
\lim_{x \to a} f(x) = L,
\]

if and only if for every \(\epsilon > 0\) there exists a \(\delta > 0\) such that whenever \(0 < |x - a| < \delta,\) it follows that \(|f(x) - L| < \epsilon.\)

In other words, the epsilon-delta framework “measures” how close the output of the function \( f(x) \) stays to the limit value \( L \) as its input \( x \) gets close to \( a.\) The parameters \(\epsilon\) (a small positive number) and \(\delta\) (another small positive number) quantify this closeness: \(\epsilon\) controls how tightly we want \( f(x) \) to cluster around \( L \), and \(\delta\) is chosen to ensure that whenever \( x \) is within \(\delta\)-distance of \( a,\) \( f(x) \) is forced to lie within \(\epsilon\)-distance of \( L.\)

**2. Can you prove the epsilon-delta theorem?**

The phrase "epsilon-delta theorem" is not a standardized name for a single, specific theorem. Typically, what is meant is either:

1. **Uniqueness of Limits Theorem:** If a limit exists, it is unique.
2. **Equivalence of Different Limit Definitions:** Showing that the intuitive idea of a limit matches the epsilon-delta definition.
3. **A Standard Epsilon-Delta Proof of a Specific Limit:** Demonstrating, using the epsilon-delta definition, that a certain limit statement is true (for example, proving \(\lim_{x \to a} (mx + b) = ma + b\)).

Below, we provide two common epsilon-delta proofs: one proving the uniqueness of limits, and another as an example of how to verify a simple linear limit using epsilon-delta techniques.

---

**A. Proof of Uniqueness of Limits (a common "epsilon-delta theorem")**

**Theorem:** If \(\lim_{x \to a} f(x) = L\) and \(\lim_{x \to a} f(x) = M\), then \(L = M.\)

**Proof:**

1. Assume, for the sake of contradiction, that \( L \neq M \).
2. Since \( L \) and \( M \) are distinct real numbers, let \(\epsilon = \frac{|L - M|}{2} > 0.\)
3. Because \(\lim_{x \to a} f(x) = L,\) by the epsilon-delta definition, there exists \(\delta_1 > 0\) such that if \(|x - a| < \delta_1,\) then \(|f(x) - L| < \epsilon.\)
4. Similarly, because \(\lim_{x \to a} f(x) = M,\) there exists \(\delta_2 > 0\) such that if \(|x - a| < \delta_2,\) then \(|f(x) - M| < \epsilon.\)
5. Let \(\delta = \min(\delta_1, \delta_2).\) If \(|x - a| < \delta,\) then both conditions hold simultaneously:
   - \(|f(x) - L| < \epsilon\)
   - \(|f(x) - M| < \epsilon\)

6. By the triangle inequality, consider:
   \[
   |L - M| = |(L - f(x)) + (f(x) - M)| \leq |L - f(x)| + |f(x) - M| < \epsilon + \epsilon = 2\epsilon.
   \]
   But we chose \(\epsilon = \frac{|L - M|}{2}\), so
   \[
   |L - M| < 2\cdot\frac{|L - M|}{2} = |L - M|.
   \]

7. This is a contradiction (it states \(|L - M| < |L - M|\), which is impossible).

Thus, our assumption that \(L \neq M\) was wrong, and hence \(L = M.\)

This proof uses the epsilon-delta logic to show that no two different limits can exist at the same point, ensuring the uniqueness of the limit.

---

**B. Example of an Epsilon-Delta Proof for a Specific Limit**

**Theorem:** Prove that \(\lim_{x \to a} (mx + b) = ma + b\) where \(m, b,\) and \(a\) are real numbers.

**Proof:**

1. We want to show that for every \(\epsilon > 0,\) there exists a \(\delta > 0\) such that if \(|x - a| < \delta,\) then \(|(mx + b) - (ma + b)| < \epsilon.\)

2. Note:
   \[
   |(mx + b) - (ma + b)| = |m(x - a)|.
   \]
   We can simplify this to:
   \[
   |m||x - a|.
   \]

3. We want \(|m||x - a| < \epsilon.\) To ensure this, we can choose:
   \[
   \delta = \frac{\epsilon}{|m|}, \quad \text{if } m \neq 0.
   \]

   If \(m = 0,\) the problem is even simpler since \(|(mx+b)-(ma+b)|=0\) always, and the limit is trivially \(b\).

4. Assuming \(m \neq 0,\) if we let \(\delta = \frac{\epsilon}{|m|},\) then whenever \(|x - a| < \delta,\)
   \[
   |(mx+b)-(ma+b)| = |m||x - a| < |m|\delta = |m|\frac{\epsilon}{|m|} = \epsilon.
   \]

5. This completes the proof: For every \(\epsilon > 0\), choosing \(\delta = \epsilon/|m|\) guarantees the desired inequality, confirming the limit is indeed \(ma + b.\)

---

**Summary:**

- The epsilon-delta definition encapsulates the precise notion of the limit.
- Using epsilon-delta arguments, we can prove fundamental theorems about limits, such as the uniqueness of a limit and straightforward computations of limits of elementary functions.
- These proofs rely heavily on carefully choosing \(\delta\) in terms of \(\epsilon\) to control how close inputs must be to the limit point to achieve a desired closeness of outputs to the limit value.