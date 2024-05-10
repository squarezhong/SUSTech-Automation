# CLASS 6 Sequential Logic

[toc]



### Maximum Clock Frequency

$\displaystyle T_{Cmin} = t_{setup} + t_{ffpd(max)} + t_{comb(max)}$

$\displaystyle f_c = \frac{1}{T_c} \le \frac{1}{t_{setup} + t_{ffpd(max)} + t_{comb(max)}}$



![Worst Timing Case](img/class6/worst_timing_case.png)

#### Setup and Hold-time Violation

- Setup-time margin > 0

  $t_{clk} - t_{ffpd}(max) - t_{comb}(max) - t_{setup}$ 

  (ffpd: flip-flop propagation delay)

- Hold-time margin > 0

  $t_{ffpd}(min) + t_{comb}(min) - t_{hold}$



### Multibit Registers and Latches



### Constructing Counters

- Given Modulo-N counters, construct a Modulo-M counter

  - N > M

    1. Asynchronous reset: State S~M~ -> S~0~ (immediately)
    2. Synchronous reset: State S~M-1~ -> S~0~

  - N < M

    multiple modulo-N counters



![74x163](img/class6/74x163.png)

![variations_of_163](img/class6/variations_of_163.png)



### Shift Register

![Shift Register by JK](img/class6/shift_register_with_jk.png)

![74x194](img/class6/msi_74x194.png)

#### Self-correcting (Ring) Counter

![](img/class6/slef_corr_counter_nand.png)

[Back to Outline](courses/EE202-17.md)
