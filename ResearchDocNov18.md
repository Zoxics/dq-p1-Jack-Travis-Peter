Jack’s hypothesis: As qubit count increases, CLOPS will decrease unless classical control-system capacity increases faster than qubit count.

[https\://github.com/Zoxics/dq-p1-Jack-Travis-Peter](https://github.com/Zoxics/dq-p1-Jack-Travis-Peter)

[https\://chatgpt.com/s/t\_6afbaf302a2c8191bc7f82524ff3584c](https://chatgpt.com/s/t_6afbaf302a2c8191bc7f82524ff3584c)

[https\://docs.google.com/spreadsheets/d/1S17b-ry3D2u7sL-ecWy8PK5BCLdo27cu7WzTdfhSWKU/edit?gid=323866149\#gid=323866149](https://docs.google.com/spreadsheets/d/1S17b-ry3D2u7sL-ecWy8PK5BCLdo27cu7WzTdfhSWKU/edit?gid=323866149#gid=323866149)

[https\://docs.google.com/presentation/d/13SFSugCzf74FJurIL4b5OB2u8zJXvWs72zKn\_OR\_5ms/edit?usp=sharing](https://docs.google.com/presentation/d/13SFSugCzf74FJurIL4b5OB2u8zJXvWs72zKn_OR_5ms/edit?usp=sharing) 

## **1\. Our research question and hypothesis**

**Research question:** How does classical control affect quantum-computer throughput as systems grow?

**Jack’s original hypothesis:**

> As qubit count increases, CLOPS will decrease unless classical control-system capacity increases faster than qubit count.

Our approach is to **read published evidence**, compare reported measurements, and evaluate which parts of this hypothesis the evidence supports.

We should separate three claims:

1. Classical control can bottleneck quantum-computer throughput.  
2. Larger systems can experience lower CLOPS because of control overhead.  
3. Avoiding that decrease requires control capacity to grow **faster than qubit count**.

Evidence for the first two does not automatically establish the third.


## **3\. How we test the hypothesis using literature**

For each source, ask:

1. What was measured?  
2. What changed between systems or experiments?  
3. Were the benchmark settings comparable?  
4. Was control capacity measured independently?  
5. Does the result support the mechanism, the qubit-count trend, or the exact scaling requirement?

Our evidence includes **three research papers**, a manufacturer’s reported benchmark comparison, and technical background. These sources have different evidentiary roles; they are not all controlled CLOPS scaling experiments.

## **4\. Research evidence**

### **A. Direct CLOPS measurements: Wack and colleagues**

The original CLOPS paper reports:

| IBM system | Total processor qubits | Quantum volume | CLOPS |
| ----- | ----- | ----- | ----- |
| ibmq\_bogota | 5 | 32 | 1,419 |
| ibmq\_toronto | 27 | 32 | 951 |
| ibmq\_brooklyn | 65 | 32 | 753 |

All three used the same quantum-volume benchmark size: **five-qubit, five-layer circuits**, with 100 shots. Thus, this compares different-sized processors running similarly sized circuits—not circuits growing from 5 to 65 active qubits.

Its timing breakdown is particularly useful:

| System | Total time, seconds | Runtime compilation and data transfer, seconds |
| ----- | ----- | ----- |
| Bogota | 352.2 | 324.7 |
| Toronto | 525.7 | 498.4 |
| Brooklyn | 663.6 | 636.6 |

See Figures 4–5 and Section IV. Classical preparation and transfer dominated elapsed time. The authors connect larger-system overhead to initializing and loading control electronics.

**Interpretation:** Supports a classical bottleneck in these systems. It does not measure control-capacity growth or establish a universal scaling law. [arxiv.org](https://arxiv.org/html/2110.14108v2?utm_source=chatgpt.com)

### **B. Device-level compilation: Dalvi and colleagues**

*One-Time Compilation of Device-Level Instructions for Quantum Subroutines* investigates repeated compilation during hybrid quantum–classical routines.

The authors develop device-level partial compilation, allowing parameters to change without repeatedly rebuilding the complete device-level program. They demonstrate the approach on trapped-ion hardware and report speedups of up to **2.7× for small VQE problems**.

**Interpretation:** Classical software improvements can reduce total runtime. This is evidence for the proposed mechanism, but the reported speedup is **not a CLOPS measurement** and does not establish faster-than-qubit-count capacity scaling. [arxiv.org](https://arxiv.org/abs/2308.10787?utm_source=chatgpt.com)

### **C. Gate-level pre-compilation: Quetschlich and colleagues**

*Reducing the Compilation Time of Quantum Circuits Using Pre-Compilation on the Gate Level* studies recurring problems with similar circuit structures.

Its evaluations include QAOA for MaxCut and a satellite-planning case study. The authors report substantially reduced compilation time while retaining comparable compiled-circuit quality.

**Interpretation:** Reducing repeated classical work is another way to improve workflow efficiency. However, gate-level compilation savings do not necessarily fall inside a particular CLOPS timing window. This paper provides supporting context rather than a direct test of Jack’s hypothesis. [arxiv.org](https://arxiv.org/abs/2305.04941?utm_source=chatgpt.com)

### **D. A useful challenge: Rigetti’s reported measurements**

Rigetti reported the following results using 100 shots:

| System | Total processor qubits | Reported CLOPS |
| ----- | ----- | ----- |
| Aspen-11 | 40 | 844 |
| Aspen-M | 80 | 892 |

Throughput did not decrease as total processor qubit count doubled. However, the comparison does not independently quantify control-capacity growth, so it cannot directly refute Jack’s conditional claim.

This is manufacturer-reported evidence. Rigetti also cautioned that implementation differences could make its CLOPS scores incomparable with IBM’s.

**Interpretation:** Challenges the simpler claim that larger processors must always have lower CLOPS. Keep this comparison separate from the IBM results. [sec.gov](https://www.sec.gov/Archives/edgar/data/1838359/000119312522043428/d248645d425.htm?utm_source=chatgpt.com)

### **E. Benchmark definitions changed**

IBM later introduced **CLOPSₕ**, using hardware-aware layers rather than the original quantum-volume layer definition.

**Consequence:** Do not combine original CLOPS and CLOPSₕ values in one trend without establishing comparability. A higher number under a different benchmark definition does not by itself demonstrate a performance improvement. [IBM Quantum Computing Blog](https://www.ibm.com/quantum/blog/quantum-metric-layer-fidelity?utm_source=chatgpt.com)

## **5\. Our conclusion**

**The evidence supports classical control as an important throughput bottleneck, but does not establish Jack’s exact faster-than-qubit-count requirement.**

| Part of the hypothesis | Assessment |
| ----- | ----- |
| Classical processing can limit throughput | Supported by the evidence reviewed. |
| Larger processors can exhibit lower CLOPS because of control overhead | Supported in the specific IBM comparison. |
| Larger processors necessarily have lower CLOPS | Not supported as a general rule. |
| Control capacity must grow faster than qubit count | Not established by these sources. |

Our conclusion is limited by the absence of a consistent, independently measured control-capacity variable across comparable systems.

**A narrower follow-up hypothesis:**

> For comparable workloads, reducing classical compilation and communication overhead increases throughput when those overheads are the dominant bottleneck.

This preserves the mechanism behind Jack’s idea while making the claim easier to test.

## **6\. Four-slide presentation outline**

| Slide | Suggested content | Time and speaker |
| ----- | ----- | ----- |
| **1\. Question** | Original hypothesis; define CLOPS; explain why classical control matters. | Jack: 60 seconds |
| **2\. Approach** | Literature comparison; distinguish processor qubits, active qubits, and control capacity. | Travis: 30 seconds |
| **3\. Findings** | IBM table; compilation evidence; Rigetti challenge. | Travis: 30 seconds, then Peter: 30 seconds |
| **4\. Conclusion and next step** | Mechanism supported; exact scaling rule unproven; proposed controlled test. | Peter: 30 seconds |

Put short source references at the bottom of the relevant slides. Keep the detailed evidence and full references in your preparation notes.

## **7\. Practice script**

*This is a draft for rehearsal. Each person should verify the sources and adjust the wording to reflect work they personally understand.*

**Jack — approximately one minute**

“Our project asks how classical control affects quantum-computer speed as systems grow. Our hypothesis is that as qubit count increases, CLOPS will decrease unless classical control-system capacity increases faster than qubit count.

CLOPS means Circuit Layer Operations Per Second. It captures throughput, including parts of the classical processing needed to run quantum circuits.

The reasoning is that a quantum processor depends on classical systems to prepare instructions, update parameters, and move results. Those systems can become bottlenecks.

We tested the hypothesis by examining published evidence. We separated evidence that classical control matters from evidence for the stronger claim that its capacity must grow faster than qubit count.”

**Travis — approximately one minute**

“Our main benchmark source was the original CLOPS paper. We also examined two compilation studies and Rigetti’s reported results.

For each comparison, we checked the workload, benchmark definition, and whether control capacity was independently measured.

The IBM results show declining CLOPS across processors with increasing total qubit counts. Their timing breakdown identifies runtime compilation and data transfer as the dominant overhead.

An important limitation is that the IBM benchmark circuits used the same number of active qubits. This was a comparison of processor sizes, not increasing circuit widths.

The compilation studies provide another perspective: changing classical software can reduce runtime without simply adding more qubits.”

**Peter — approximately one minute**

“The evidence also limits our original claim. Rigetti reported slightly higher CLOPS on its larger processor, although the comparison does not tell us how control capacity changed.

We also found that CLOPS definitions changed over time, making some published scores unsuitable for direct comparison.

Our conclusion is that classical control can strongly limit throughput, but we have not established that its capacity must increase faster than qubit count.

A stronger next test would vary active circuit width and control resources independently while keeping the benchmark protocol consistent. We would measure compilation, communication, and execution time separately.

That would help distinguish a classical bottleneck from other reasons throughput changes.”

## **8\. Likely questions and prepared answers**

**Did you prove the original hypothesis?**

No. The reviewed evidence supports the bottleneck mechanism, but not the exact capacity-scaling requirement.

**Why does “faster than qubit count” require additional evidence?**

It specifies a growth relationship. Testing it requires independent measurements of capacity across increasing qubit counts. Observing overhead alone is insufficient.

**Does adding qubits automatically increase execution time?**

No. The effect depends on which qubits are used, the workload, parallelism, and the control architecture.

**Why are total qubits and active qubits different?**

A processor can have many qubits while a benchmark uses only a subset. Increasing processor size and increasing circuit width are different experiments.

**Does a compilation speedup equal a CLOPS speedup?**

No. The saved work must fall within the timed benchmark, and the benchmark must actually be rerun before claiming a CLOPS improvement.

**What would contradict the original hypothesis?**

A comparable scaling experiment where qubit count increases, independently measured control capacity grows no faster than qubit count, and CLOPS reliably remains stable or improves.

**Would declining CLOPS despite faster control refute it?**

Not necessarily. “Unless” proposes a necessary condition for avoiding a decrease; it does not guarantee that faster control removes every other bottleneck.

**Why not simulate this with an ordinary circuit simulator?**

A circuit simulator alone would not reproduce real control-electronics initialization, communication, and compilation overhead. Testing those effects requires an explicit performance model or hardware measurements.

## **9\. Proposed next experiment**

This is a future test, not completed work.

1. Choose one hardware family and one benchmark protocol.  
2. Increase active circuit width while controlling depth, shots, and gate density as far as practical.  
3. At each width, vary an independent control resource, such as instruction-processing throughput or communication bandwidth.  
4. Measure classical preparation, transfer, quantum execution, and total elapsed time separately.  
5. Repeat measurements to assess variation.  
6. Determine whether proportional capacity growth is sufficient, or whether faster growth is required.

Define “capacity” before collecting data. Do not infer capacity from CLOPS itself.

## **10\. Final preparation checklist**

* All three members agree on the conclusion.  
* Everyone can explain the evidence and its limitations.  
* Four slides are complete with citations.  
* Literature notes and slides are in the shared repository.  
* README includes the method, findings, and limitations.  
* Architecture-tab team details are complete.  
* Speaking time is approximately equal.  
* Full rehearsal finishes within three minutes.  
* Everyone can answer at least one likely question.  
* Separately complete the assigned GitHub workflow and IBM lessons.

## **11\. Reference list**

1. **Wack et al. (2021).** *Quality, Speed, and Scale: three key attributes to measure the performance of near-term quantum computers.* Especially Figures 4–5 and Section IV.  
   [https\://arxiv.org/abs/2110.14108](https://arxiv.org/abs/2110.14108?utm_source=chatgpt.com)  
2. **Dalvi et al. (2023; revised 2024).** *One-Time Compilation of Device-Level Instructions for Quantum Subroutines.*  
   [https\://arxiv.org/abs/2308.10787](https://arxiv.org/abs/2308.10787?utm_source=chatgpt.com)  
3. **Quetschlich, Burgholzer, and Wille (2023).** *Reducing the Compilation Time of Quantum Circuits Using Pre-Compilation on the Gate Level.*  
   [https\://arxiv.org/abs/2305.04941](https://arxiv.org/abs/2305.04941?utm_source=chatgpt.com)  
4. **Rigetti (February 15, 2022).** *Rigetti Computing Announces Commercial Availability of 80-Qubit Aspen-M System and Results of CLOPS Speed Tests.* Manufacturer announcement reproduced in an SEC filing.  
   [https\://www\.sec.gov/Archives/edgar/data/1838359/000119312522043428/d248645d425.htm](https://www.sec.gov/Archives/edgar/data/1838359/000119312522043428/d248645d425.htm?utm_source=chatgpt.com)  
5. **Wack and McKay, IBM (November 20, 2023).** *Updating how we measure quantum quality and speed.* Technical explanation of CLOPSₕ.  
   [https\://www\.ibm.com/quantum/blog/quantum-metric-layer-fidelity](https://www.ibm.com/quantum/blog/quantum-metric-layer-fidelity?utm_source=chatgpt.com)  
6. **Gambetta et al., IBM (November 1, 2021).** *Driving quantum performance.* Background on the hardware and software components affecting CLOPS.  
   [https\://www\.ibm.com/quantum/blog/circuit-layer-operations-per-second](https://www.ibm.com/quantum/blog/circuit-layer-operations-per-second?utm_source=chatgpt.com)

