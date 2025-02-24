# CSIT5970 Assignment-1: EC2 Measurement (2 questions, 4 marks)

### Deadline: 11:59PM, Feb, 28, Friday

---

### Name: Yang Zhuorui 
### Student Id: 21095046
### Email: zyangdm@connect.ust.hk

---

## Question 1: Measure the EC2 CPU and Memory performance

1. (1 mark) Report the name of measurement tool used in your measurements (you are free to choose *any* open source measurement software as long as it can measure CPU and memory performance). Please describe your configuration of the measurement tool, and explain why you set such a value for each parameter. Explain what the values obtained from measurement results represent (e.g., the value of your measurement result can be the execution time for a scientific computing task, a score given by the measurement tools or something else).

    1. **Measurement Tool**:

       - **Name**: The tool used for measuring CPU and memory performance is **Sysbench**, an open-source, cross-platform benchmarking tool. It is widely used for evaluating system performance, particularly for CPU, memory, and database workloads.

    2. **Configuration of the Measurement Tool**:
 
        - **CPU Performance**:
        - Command: `sysbench cpu --cpu-max-prime=20000 run`
        - Explanation: This parameter sets the upper limit for calculating prime numbers. A higher value increases the computational load, making the test more intensive. The value `20000` is chosen to ensure the test is sufficiently demanding to evaluate CPU performance.
          
        - **Memory Performance**:
        - Command: `sysbench memory --memory-block-size=1M --memory-total-size=10G run`
        - Explanation: The `--memory-block-size` parameter sets the size of the memory blocks to be allocated, and `--memory-total-size` sets the total amount of memory to be tested. These values ensure that the memory performance is tested under significant load.

    3. **Explanation of Measurement Results**:

        - **CPU Performance**:
        - The result will include metrics like the total execution time and the number of events per second. These values represent how efficiently the CPU can handle computational tasks.

        ![CPU Performance](https://github.com/user-attachments/assets/5f63d84b-b350-4099-8cf5-7b8d37e9b5c3)

        - **Memory Performance**:
        - The result will include metrics like the total amount of transferred data and the transfer rate. These values indicate the speed and efficiency of memory operations.

        ![Memory Performance](https://github.com/user-attachments/assets/2e8801da-306e-4135-ae41-48d57f6f352d)


2. (1 mark) Run your measurement tool on general purpose `t2.micro`, `t2.medium`, and `c5d.large` Linux instances, respectively, and find the performance differences among these instances. Launch all the instances in the **US East (N. Virginia)** region. Does the performance of EC2 instances increase commensurate with the increase of the number of vCPUs and memory resource?

    1. **CPU Performance**:
       **c5d.large** shows lower CPU performance at **456.56/s**, which could be attributed to its optimization for specialized high-performance computing tasks rather than general-purpose CPU benchmarks.

    2. **Memory Performance**:
       **t2.micro** and **t2.medium** demonstrate comparable memory performance, with operation rates of **18669.36/s** and **18994.58/s**, respectively.
       **c5d.large** achieves significantly higher memory performance at **20522.43/s**, indicating superior efficiency in memory operations.

    3. **Conclusion**

       **CPU Performance**: The CPU performance of **t2.micro** and **t2.medium** is nearly identical, while **c5d.large** underperforms in this specific CPU benchmark.
       **Memory Performance**: **c5d.large** outperforms both **t2.micro** and **t2.medium** in memory performance, showcasing its enhanced memory handling capabilities.

    4. **Measurement Results Table**

        To complete the analysis, fill in the table below with the corresponding measurement results for each instance type:

        | Instance Type | CPU Performance (events/s) | Memory Performance (operations/s) |
        |---------------|----------------------------|-----------------------------------|
        | t2.micro      | 876.55                     | 18669.36                          |
        | t2.medium     | 877.97                     | 18994.58                          |
        | c5d.large     | 456.56                     | 20522.43                          |

        This table summarizes the performance differences across the three instance types, highlighting the strengths and weaknesses of each in terms of CPU and memory performance.

## Question 2: Measure the EC2 Network performance

1. (1 mark) The metrics of network performance include **TCP bandwidth** and **round-trip time (RTT)**. Within the same region, what network performance is experienced between instances of the same type and different types? In order to answer this question, you need to complete the following table.

    1. **TCP Bandwidth**:
          - Instances of type `m5.large` and `c5n.large` demonstrate significantly higher TCP bandwidth compared to `t3.medium` instances.
          - The bandwidth between `m5.large` and `c5n.large` instances is nearly identical, suggesting comparable network performance capabilities.

    2. **Round-Trip Time (RTT)**:
          - Instances of type `m5.large` and `c5n.large` exhibit much lower RTT values compared to `t3.medium` instances, reflecting faster response times.
          - The RTT between instances of the same type is generally lower than between instances of different types, with the exception of `t3.medium` instances, which consistently show higher RTT values.


        ### Summary Table:

        | Type                      | TCP Bandwidth (Mbps) | RTT (ms) |
        | ------------------------- | -------------------- | -------- |
        | `t3.medium` - `t3.medium` | 10400                | 1.132    |
        | `m5.large` - `m5.large`   | 51000                | 0.294    |
        | `c5n.large` - `c5n.large` | 50800                | 0.287    |
        | `t3.medium` - `c5n.large` | 10600                | 0.797    |
        | `m5.large` - `c5n.large`  | 48500                | 0.693    |
        | `m5.large` - `t3.medium`  | 11500                | 1.166    |



2. (1 mark) What about the network performance for instances deployed in different regions? In order to answer this question, you need to complete the following table.



    1. **TCP Bandwidth**:
          - The TCP bandwidth between instances located in the same region (e.g., N. Virginia - N. Virginia and Oregon - Oregon) is significantly higher than between instances in different regions (e.g., N. Virginia - Oregon).
          - The highest bandwidth is observed between instances in Oregon, reaching **95300 Mbps**, followed by instances in N. Virginia with **49700 Mbps**.

    2. **Round-Trip Time (RTT)**:
          - The RTT is considerably lower for instances within the same region compared to instances in different regions.
          - The RTT between N. Virginia and Oregon is **62.866 ms**, which is significantly higher than the RTT within the same region (e.g., **0.217 ms** for N. Virginia and **0.102 ms** for Oregon). This is due to the geographical distance between the two regions.


        ### Summary Table:

        | Connection                | TCP Bandwidth (Mbps) | RTT (ms) |
        | ------------------------- | -------------------- | -------- |
        | N. Virginia - Oregon      | 596                  | 65.336   |
        | N. Virginia - N. Virginia | 51300                | 0.256    |
        | Oregon - Oregon           | 94600                | 0.125    |




