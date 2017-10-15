
# Chapter II. Elements of Signal Detection Theory

## II.1 Introduction

### Introduction

* Signal detection = the problem of deciding which
signal is present from 2 or more possibilities
    * one possibility may be that there is no signal

* Based on **noisy** observations
    * signals are affected by noise

### The model for signal detection

![Signal detection model](img/SignalDetectionModel.png){#id .class width=60%}

* Contents:
    * Information source: generates messages $a_n$ with probabilities $p(a_n)$
    * Modulator: transmits a signal $s_n(t)$ for message $a_n$
    * Channel: adds random noise
    * Sampler: takes samples from the signal $s_n(t)$
    * Receiver: **decides** what message $a_n$ has been transmitted

### Practical scenarios

* Data transmission
    * binary voltage levels (e.g. $s_n(t)$ = constant)
    * PSK modulation (Phase Shift Keying): $s_n(t)$ = cosine with same frequency but various initial phase
    * FSK modulation (Frequency Shift Keying): $s_n(t)$ = cosines with different frequencies

* Radar
    * a signal is emitted; if there is an obstacle, the signal gets reflected back
    * the receiver waits for possible reflections of the signal and must decide
        * no reflection is present -> no object
        * reflected signal is present -> object detected

### Generalizations

* Decide between more than two signals

* Number of observations:
    * use only one sample
    * use multiple samples
    * observe the whole continuous signal for some time $T$


## II.2 Detection of constant signals

### Detection of a constant signal, white normal noise, 1 sample

* Simplest case: detection of a constant signal contaminated with white normal noise, using 1 sample
    * two messages $a_0$ and $a_1$
    * messages are encoded as constant signals
        * for $a_0$: send $s_0(t) = 0$
        * for $a_1$: send $s_1(t) = A$
    * over the signals there is white noise, normal distribution $\mathcal{N}(0, \sigma^2)$
    * receiver takes just 1 sample
    * decision: compare sample with a threshold

### Decision

* The value of the sample taken is $r = s + n$
    * $s$ is the true underlying signal ($s_0 = 0$ or $s_1 = A$)
    * $n$ is a sample of the noise

* $n$ is a (continuous) random variable, with normal distribution
* $r$ is a random variable also
    * what distribution does it have?

* Decision is taken by comparing with a threshold $T$:
    * if $r < T$,  take decision $D_0$: decide the true signal is $s_0$
    * if $r \geq T$,  take decision $D_1$: decide the true signal is $s_1$

### Hypotheses 

* Receiver chooses between **two hypotheses**:
    * $H_0$: true signal is $s_0$ ($a_0$ has been transmitted)
    * $H_1$: true signal is $s_1$ ($a_1$ has been transmitted)

* Possible results
    1. No signal present, no signal detected.
        * Decision $D_0$ when hypothesis is $H_0$
        * Probability is $P(D_0 \cap H_0)$
    2. **False alarm**: no signal present, signal detected (error)
        * Decision $S_1$ when hypothesis is $H_0$
        * Probability is $P(D_1 \cap H_0)$
    3. **Miss**: signal present, no signal detected (error)
        * Decision $D_0$ when hypothesis is $H_1$
        * Probability is $P(D_0 \cap H_1)$
    4. Signal detected correctly: signal present, signal detected
        * Decision $D_1$ when hypothesis is $H_1$
        * Probability is $P(D_1 \cap H_1)$


### Maximum likelihood criterion

* Choose the hypothesis that **seems most likely** given the observed
sample $r$

* The **likelihood** of an observation $r$ = 
the probability density of $r$ given a hypothesis $H_0$ or $H_1$

* Likelihood in case of hypothesis $H_0$: $w(r | H_0)$ 
    * $r$ is only noise, so value is taken from the noise distribution 

* Likelihood in case of hypothesis $H_1$: $w(r | H_1)$
    * $r$ is A + noise,  so value is taken from the distribution of (A + noise)

* Likelihood test:
$$\frac{w(r | H_1)}{w(r | H_0)} \grtlessH 1$$

### Graphical interpretation

* Consider noise having a normal distribution

* Plot the two density functions for $H_0$, $H_1$

### Decision via threshold

* Decision via ML = comparing $r$ with a threshold $T$
* The threshold = the cross-over point of the two distributions

### Normal noise

* Particular case: the noise has normal distribution $\mathcal{N}(0,\sigma^2)$

* Likelihood test is $\frac{w(r|H_1)}{r|H_0} = \frac{e^{\frac{(r-A)^2}{2\sigma^2}}}{e^{\frac{r^2}{2\sigma^2}}} \grtlessH 1$
    * this ratio is usually called **likelihood ratio**

* For normal distribution, it is easier to apply *natural logarithm* to the terms
    * logarithm is a monotonic increasing function, so it won't change the comparison
    * if A < B, then $log(A) < log(B)$

* The **log-likelihood** of an observation = the logarithm of the likelihood value
    * usually the natural logarithm, but any one can be used

### Log-likelihood test for ML

* For normal noise, the ML decision means the log-likelihood test
$$\frac{(r-A)^2}{r^2} \grtlessH 1$$

* Applying square root 
$$\frac{|r-A|}{|r|} \grtlessH 1$$

* $|r-A|$ = distance from $r$ to $A$, $|r|$ = distance from $r$ to $0$

* ML decision with normal noise: choose the value 0 or A  which is **nearest** to $r$
    * very general principle, encountered in many other scenarios
    * also known as **nearest neighbor** principle / decision
    * equivalent with setting a threshold $T = \frac{A}{2}$ 

### Generalizations

* What if the noise has another distribution?
    * Threshold $T$ is still the cross-over point, whatever that is

* What if the noise distributions are different for $H_0$ and $H_1$? 
    * Threshold $T$ is the cross-over point, whatever that is

* What if the signal $s_0(t)$ (for $H_0$) is not 0, but another constant value B?
    * $T$ is the crossover point, the distributions are centered on B and A
    * In case of normal noise, choose B or A whichever is nearest (threshold is at middle point)

### Generalizations

* What if we have more than two signal levels?
    * e.g. 4 possible signals: -6, -2, 2, 6
    * Just choose the most likely hypothesis, out of 4 likelihood functions 
    * Not a single threshold value, now there are more

### Pitfalls of ML decision

* The ML is based on comparing **conditional** probability density functions
    * conditioned by $H_0$ or by $H_1$

* Conditioning by $H_0$ and $H_1$ ignores the probability of $H_0$ or $H_1$ actually happening

* Reminder: the Bayes rule
$$P(A \cap B) = P(B | A) \cdot P(A))$$

* Interpretation
    * The probability $P(A)$ is taken out from $P(B|A)$
    * $P(B|A)$ gives no information  on $P(A)$, the chances of $A$ actually happening
    * Example: P(score | shoot)
* Practical: if $p(H_0) >> p(H_1)$, we may want to move the threshold towards $H_1$

### The minimum error probability criterion

* Takes into account the probabilities $P(H_0)$ and $P(H_1)$

* Goal is to **minimize the total probability of error $P_e$**
    * errors = false alarms and misses

* Consider we have a threshold $T$ such that
    * we decide $D_0$ when $r<T$
    * we decide $D_1$ when $r \geq T$

* We need to find $T$

### Probability of error

* Probability of false alarm
$$\begin{split}
P(D_1 \cap H_0) =& P(D_1 | H_0) \cdot P(H_0)\\
=& \int_T^{\infty} w(r | H_0) dx \cdot P(H_0)\\
=& (1 - \int_{-\infty}^T w(r | H_0) dx \cdot P(H_0)
\end{split}$$

* Probability of miss
$$\begin{split}
P(D_0 \cap H_1) =& P(D_0 | H_1) \cdot P(H_1)\\
=& \int_{-\infty}^T w(r | H_1) dx \cdot P(H_1)
\end{split}$$

* The sum is
$$P_e = P(H_0) + \int_{-\infty}^T [w(r|H_1) \cdot P(H_1) - w(r|H_0) \cdot P(H_0)] dx$$

### Minimum probability of error

* We want to minimize $P_e$, i.e. to minimize the integral

* To minimize the integral, we choose $T$ such that for all $r < T$, 
the term below the integral is **negative**
    * because integrating over all the interval where the function is negative ensures minimum value of integral

* So, when $w(r|H_1) \cdot P(H_1) - w(r|H_0) \cdot P(H_0) < 0$ we have $r < T$, i.e. decision $D_0$
* Conversely, When $w(r|H_1) \cdot P(H_1) - w(r|H_0) \cdot P(H_0) > 0$ we have $r > T$, i.e. decision $D_1$

* Therefore
$$w(r|H_1) \cdot P(H_1) - w(r|H_0) \cdot P(H_0) \grtlessH 0$$
$$\frac{w(r | H_1)}{w(r | H_0)} \grtlessH \frac{P(H_0}{P(H_1)}$$

### Interpretation

* Similar to ML, but threshold depends on probabilities of the two hypotheses
    * When one hypotheses is more likely than the other, the threshold
    is pushed in its favor, towards the other




### Minimum risk (cost) criterion

* How to choose the threshold? We need criteria
    * In general: how to delimit regions $R_i$?

* Minimum risk (cost) criterion: assign costs to decisions, minimize average cost
    * $C_{ij}$ = cost of decision $D_i$ when symbol was $a_j$
    * $C_{00}$ = cost for good $a_0$ detection
    * $C_{10}$ = cost for false alarm
    * $C_{01}$ = cost for miss
    

*  The risk = the average cost
$$R = C_{00} P(D_0 \cap a_0) + C_{10} P(D_1 \cap a_0) + C_{01} P(D_0 \cap a_1) + C_{11} P(D_1 \cap a_1)$$

* Minimum risk criterion: **minimize the risk R**

### Computations

* Proof on table:
    * Use Bayes rule
    * Notations: $w(r | a_j)$ (*likelihood*)
    * Probabilities: $\int_{R_i} w(r | a_j) dV$

* Conclusion, **decision rule is**
$$\frac{w(r|a_1)}{w(r|a_0)} \gtrless \frac{(C_{10}-C_{00})p(a_0)}{(C_{01}-C_{11})p(a_1)}$$
$$\Lambda(r) \gtrless K$$

* Interpretation: effect of costs, probabilities (move threshold)

* Can also apply logarithm (useful for normal distribution)
$$\ln \Lambda(r) \gtrless \ln K$$

* Example at blackboard: random noise with $N(0, \sigma^2)$, one sample

### Ideal observer criterion

* Minimize the probability of decision error $P_e$
    * definition of $P_e$

* Particular case of minimum risk, with
    * $C_{00} = C_{11} = 0$ (good decisions bear no cost)
    * $C_{10} = C_{01}$ (pay the same in case of bad decisions)

$$\frac{w(r|a_1)}{w(r|a_0)} \gtrless \frac{p(a_0)}{p(a_1)}$$

### Maximum likelihood criterion

* Particular case of above, with equal probability of messages

$$\frac{w(r|a_1)}{w(r|a_0)} \gtrless 1$$
$$\ln \frac{w(r|a_1)}{w(r|a_0)} \gtrless 0$$

* Example at blackboard: random noise with $N(0, \sigma^2)$, one sample
* Example at blackboard: random noise with $N(0, \sigma^2)$, **two** samples