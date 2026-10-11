# OSTEP Ch.4 Homework Answers

## Q1
- Prediction / 预测: the state table is below.
```
Time  PID 0       PID 1     CPU  IOs
1     (running)   (ready)   1    0
2     (running)   (ready)   1    0
3     (running)   (ready)   1    0
4     (running)   (ready)   1    0
5     (running)   (ready)   1    0
6     (done)      (running) 1    0
7     (done)      (running) 1    0
8     (done)      (running) 1    0
9     (done)      (running) 1    0
10    (done)      (running) 1    0
```
- Reasoning / 理由:两个进程都需要100%的CPU利用率，没有I/O操作。先执行PID 0 运行5个tick，PID 0运行结束后再运行PID 1 运行5个tick。CPU在这个过程中没有空闲。
- Verified result / 验证结果:CPU Busy 10 (100.00%) IO Busy  0 (0.00%)
- Analysis / 分析:两个进程都需要100%的CPU利用率，没有I/O操作。所以CPU的利用率是100%。所以没有预测错误。

## Q2
- Prediction / 预测: the state table is below.
```
Time  PID 0     PID 1       CPU  IOs
1     (running) (ready)     1    0
2     (running) (ready)     1    0
3     (running) (ready)     1    0
4     (running) (ready)     1    0  
5     (done)    RUN:io      1    0
6     (done)    (blocked)   0    1
7     (done)    (blocked)   0    1
8     (done)    (blocked)   0    1
9     (done)    (blocked)   0    1
10    (done)    (blocked)   0    1
11*   (done)    RUN:io_done 1    0
```
- Reasoning / 理由:系统先调度PID 0运行4个tick的CPU。PID 1准备就绪并在第5个tick发起I/O。PID 1的I/O需要1个tick的CPU完成，之后PID 1变为阻塞状态，阻塞状态运行5个tick后在第11个tick完成l/O占用1个tick的CPU，CPU 6tick（54.55%）I/Os 5tick（45.45%）。
- Verified result / 验证结果:CPU Busy 6 (54.55%) IO Busy  5 (45.45%)
- Analysis / 分析:系统先调度PID 0运行4个tick的CPU。PID 1准备就绪并在第5个tick发起I/O。PID 1的I/O需要1个tick的CPU完成，之后PID 1变为阻塞状态，阻塞状态运行5个tick后在第11个tick完成l/O占用1个tick的CPU。所以没有预测错误。

## Q3
- Prediction / 预测: the state table is below.
```
Time  PID 0        PID 1       CPU  IOs
1     RUN:io       (ready)     1    0
2     (blocked)    (running)   1    1
3     (blocked)    (running)   1    1
4     (blocked)    (running)   1    1
5     (blocked)    (running)   1    1
6     (blocked)    (done)      0    1
7*    RUN:io_done  (done)      1    0
```
- Reasoning / 理由:系统先调度PID 0发起I/O占用1个tick的CPU，PID 0进入阻塞状态5个tick。在第一个tick的时候PID 1准备就绪，然后在PID 0进入阻塞状态的时候运行4个tick的CPU，在第6个tick完成，第7个tick PID 0完成I/O。CPU 6tick（85.71%）I/Os 5tick（71.43%）。
- Verified result / 验证结果:CPU Busy 6 (85.71%) IO Busy  5 (71.43%)
- Analysis / 分析:系统先调度PID 0发起I/O占用1个tick的CPU，PID 0进入阻塞状态5个tick。在第一个tick的时候PID 1准备就绪，然后在PID 0进入阻塞状态的时候运行4个tick的CPU，在第6个tick完成，第7个tick PID 0完成I/O。所以没有预测错误。

## Q4
- Prediction / 预测: the state table is below.
```
Time  PID 0        PID 1       CPU  IOs
1     RUN:io       (ready)     1    0
2     (blocked)    (ready)     0    1
3     (blocked)    (ready)     0    1
4     (blocked)    (ready)     0    1
5     (blocked)    (ready)     0    1
6     (blocked)    (ready)     0    1
7*    RUN:io_done  (ready)     1    0
8     (done)       (running)   1    0
9     (done)       (running)   1    0
10    (done)       (running)   1    0
11    (done)       (running)   1    0
```
- Reasoning / 理由:系统先调度PID 0发起I/O占用1个tick的CPU，PID 0进入阻塞状态5个tick。因为等待I/O的时候不能切换，所以期间PID 1保持准备就绪。在第7个tick完成I/O占用一个tick CPU后PID 1运行4个tick的CPU。CPU 6tick（54.55%）I/Os 5tick（45.45%）。
- Verified result / 验证结果:CPU Busy 6 (54.55%) IO Busy  5 (45.45%)
- Analysis / 分析:系统先调度PID 0发起I/O占用1个tick的CPU，PID 0进入阻塞状态5个tick。因为等待I/O的时候不能切换，所以期间PID 1保持准备就绪。在第7个tick完成I/O占用一个tick CPU后PID 1运行4个tick的CPU。所以没有预测错误。

## Q5
- Prediction / 预测: the state table is below.
```
Time  PID 0        PID 1       CPU  IOs
1     RUN:io       (ready)     1    0
2     (blocked)    (running)   1    1
3     (blocked)    (running)   1    1
4     (blocked)    (running)   1    1
5     (blocked)    (running)   1    1
6     (blocked)    (done)      0    1
7*    RUN:io_done  (done)      1    0
```
- Reasoning / 理由:Q5 与 Q4 不同，默认SWITCH_ON_IO 时，CPU在第2个tick会去运行PID 1，总时间为7个tick，少了4个tick的时间。CPU 6tick（85.71%）I/Os 5tick（71.43%）。
- Verified result / 验证结果:CPU Busy 6 (85.71%) IO Busy  5 (71.43%)
- Analysis / 分析:Q5 与 Q4 不同，默认SWITCH_ON_IO 时，CPU在第2个tick会去运行PID 1，总时间为7个tick，少了4个tick的时间。所以没有预测错误。

## Q6
- Prediction / 预测: the state table is below.
```
Time  PID 0        PID 1        PID 2      PID 3      CPU  IOs
1     RUN:io       (ready)      (ready)    (ready)    1    0
2     (blocked)    (running)    (ready)    (ready)    1    1
3     (blocked)    (running)    (ready)    (ready)    1    1
4     (blocked)    (running)    (ready)    (ready)    1    1
5     (blocked)    (running)    (ready)    (ready)    1    1
6     (blocked)    (running)    (ready)    (ready)    1    1
7*    RUN:io_done  (done)       (ready)    (ready)    1    0
8     (ready)      (done)       (running)  (ready)    1    0
9     (ready)      (done)       (running)  (ready)    1    0
10    (ready)      (done)       (running)  (ready)    1    0
11    (ready)      (done)       (running)  (ready)    1    0
12    (ready)      (done)       (running)  (ready)    1    0
13    (ready)      (done)       (done)     (running)  1    0
14    (ready)      (done)       (done)     (running)  1    0
15    (ready)      (done)       (done)     (running)  1    0
16    (ready)      (done)       (done)     (running)  1    0
17    (ready)      (done)       (done)     (running)  1    0
18    RUN:io       (done)       (done)     (done)     1    0
19    (blocked)    (done)       (done)     (done)     0    1
20    (blocked)    (done)       (done)     (done)     0    1
21    (blocked)    (done)       (done)     (done)     0    1
22    (blocked)    (done)       (done)     (done)     0    1
23    (blocked)    (done)       (done)     (done)     0    1
24*   RUN:io_done  (done)       (done)     (done)     1    0
25    RUN:io       (done)       (done)     (done)     1    0
26    (blocked)    (done)       (done)     (done)     0    1
27    (blocked)    (done)       (done)     (done)     0    1
28    (blocked)    (done)       (done)     (done)     0    1
29    (blocked)    (done)       (done)     (done)     0    1
30    (blocked)    (done)       (done)     (done)     0    1
31*   RUN:io_done  (done)       (done)     (done)     1    0
```
- Reasoning / 理由:系统先调度PID 0发起I/O占用1个tick的CPU，PID 0进入阻塞状态5个tick。在第一个tick的时候PID 1准备就绪，然后在PID 0进入阻塞状态的时候运行5个tick的CPU，在第7个tick完成，第7个tick PID 0完成I/O。8-12tick PID 2运行5个tick，在第13个tick完成，PID 3在13-17tick运行5个tick，在18tick完成，期间I/O 设备非常空闲。在18tick PID 0发起I/O，进入5个tick阻塞状态，在24tick完成I/O，25-31tick重复。CPU 21tick（67.74%）I/Os 15tick（48.39%）。
- Verified result / 验证结果:CPU Busy 21 (67.74%) IO Busy  15 (48.39%)
- Analysis / 分析:系统先调度PID 0发起I/O占用1个tick的CPU，PID 0进入阻塞状态5个tick。在第一个tick的时候PID 1准备就绪，然后在PID 0进入阻塞状态的时候运行5个tick的CPU，在第7个tick完成，第7个tick PID 0完成I/O。8-12tick PID 2运行5个tick，在第13个tick完成，PID 3在13-17tick运行5个tick，在18tick完成，期间I/O 设备非常空闲。在18tick PID 0发起I/O，进入5个tick阻塞状态，在24tick完成I/O，在25-31tick重复操作。所以没有预测错误。

## Q7
- Prediction / 预测: the state table is below.
```
Time  PID 0        PID 1        PID 2      PID 3      CPU  IOs
1     RUN:io       (ready)      (ready)    (ready)    1    0
2     (blocked)    (running)    (ready)    (ready)    1    1
3     (blocked)    (running)    (ready)    (ready)    1    1
4     (blocked)    (running)    (ready)    (ready)    1    1
5     (blocked)    (running)    (ready)    (ready)    1    1
6     (blocked)    (running)    (ready)    (ready)    1    1
7*    RUN:io_done  (done)       (ready)    (ready)    1    0
8     RUN:io       (done)       (ready)    (ready)    1    0
9     (blocked)    (done)       (running)  (ready)    1    1
10    (blocked)    (done)       (running)  (ready)    1    1
11    (blocked)    (done)       (running)  (ready)    1    1
12    (blocked)    (done)       (running)  (ready)    1    1
13    (blocked)    (done)       (running)  (ready)    1    1
14*   RUN:io_done  (done)       (done)     (ready)    1    0
15    RUN:io       (done)       (done)     (ready)    1    0
16    (blocked)    (done)       (done)     (running)  1    1
17    (blocked)    (done)       (done)     (running)  1    1
18    (blocked)    (done)       (done)     (running)  1    1
19    (blocked)    (done)       (done)     (running)  1    1
20    (blocked)    (done)       (done)     (running)  1    1
21*   RUN:io_done  (done)       (done)     (done)     1    0
```
- Reasoning / 理由:立即重新运行频繁I/O 的进程可以让CPU率最大化CPU 21tick（100%）I/Os 15tick（71.43%）。
- Verified result / 验证结果:CPU Busy 21 (100.00%) IO Busy  15 (71.43%)
- Analysis / 分析:立即重新运行频繁I/O 的进程可以让CPU率最大化。所以没有预测错误。

## Q8
- Prediction / 预测: the state table is below.
```
s1
Time  PID 0        PID 1       CPU  IOs
1     (running)    (ready)     1    0
2     RUN:io       (ready)     1    0
3     (blocked)    (running)   1    1
4     (blocked)    (running)   1    1
5     (blocked)    (running)   1    1
6     (blocked)    (done)      0    1
7     (blocked)    (done)      0    1
8*    RUN:io_done  (done)      1    0
9     RUN:io       (done)      1    0
10    (blocked)    (done)      0    1
11    (blocked)    (done)      0    1
12    (blocked)    (done)      0    1
13    (blocked)    (done)      0    1
14    (blocked)    (done)      0    1
15*   RUN:io_done  (done)      1    0

s2
Time  PID 0        PID 1       CPU  IOs
1     RUN:io       (ready)     1    0
2     (blocked)    (running)   1    1
3     (blocked)    RUN:io      1    1
4     (blocked)    (ready)     0    1
5     (blocked)    (ready)     0    1
6     (blocked)    (ready)     0    1
7*    RUN:io_done  (blocked)   1    1
8     (ready)      (blocked)   0    1
9     (ready)      (blocked)   0    1
9     (ready)      (blocked)   0    1
10    (ready)      (blocked)   0    1
11*   (ready)      RUN:io_done 1    0
12    RUN:io       (ready)     1    0
13    (blocked)    RUN:io      1    1
14    (blocked)    (ready)     0    1
15    (blocked)    (ready)     0    1
16    (blocked)    (ready)     0    1
17    (blocked)    (ready)     0    1
18*   RUN:io_done  (blocked)   1    1
19    (running)    (blocked)   1    1
20    (done)       (blocked)   0    1
21    (done)       (blocked)   0    1
22    (done)       (blocked)   0    1
23*   (done)       RUN:io_done 1    0

s3
Time  PID 0        PID 1       CPU  IOs
1     (running)    (ready)     1    0
2     RUN:io       (ready)     1    0
3     (blocked)    RUN:io      1    1
4     (blocked)    (ready)     0    1
5     (blocked)    (ready)     0    1
6     (blocked)    (ready)     0    1
7     (blocked)    (ready)     0    1
8*    RUN:io_done  (blocked)   1    1
9     (running)    (blocked)   1    1
10    (done)       (blocked)   0    1
10    (done)       (blocked)   0    1
11    (done)       (blocked)   0    1
12*   (done)       RUN:io_done 1    0
13    (done)       RUN:io      1    0
14    (done)       (blocked)   0    1
15    (done)       (blocked)   0    1
16    (done)       (blocked)   0    1
17    (done)       (blocked)   0    1
18    (done)       (blocked)   0    1
19*   (done)       RUN:io_done 1    0
20    (done)       (running)   1    0
```
- Reasoning / 理由:
s1:系统先调度PID 0运行1个tick的CPU，然后发起I/O占用1个tick的CPU，PID 0进入阻塞状态5个tick。PID 1在1-2tick保持准备就绪状态，3-5tick因为PID 0在阻塞状态所以运行3个tick的CPU，然后在6tick完成。8tick的时候PID 0完成I/O占用1个tick的CPU，9tick发起I/O占用1个tick的CPU，PID 0进入阻塞状态5个tick，在15tick完成I/O占用1个tick的CPU。CPU 8tick（53.33%）I/Os 10tick（66.67%）。
s2:系统先调度PID 0发起I/O占用1个tick的CPU，PID 0进入阻塞状态5个tick。在第一个tick的时候PID 1准备就绪，然后在PID 0进入阻塞状态的时候运行1个tick的CPU，然后发起I/O占用1个tick的CPU后，保持准备就绪到7tick时PID 0完成I/O占用1个tick的CPU的时候进入阻塞状态5个tick，在11tick时PID 1完成I/O占用1个tick的CPU，12tick时PID 0发起I/O占用1个tick的CPU并进入5个tick的阻塞状态时PID 1准备就绪，13tick时PID 1发起I/O占用1个tick的CPU并保持4个tick的准备就绪状态，18tick时PID 0完成I/O，PID 1进入阻塞状态5个tick并在23tick完成I/O。19tick时因为CPU空闲所以PID 0可以运行一个tick的CPU后完成。CPU 10tick（43.48%）I/Os 19tick（82.61%）。
s3:系统先调度PID 0运行1个tick的CPU，然后发起I/O占用1个tick的CPU，PID 0进入阻塞状态5个tick。在3tick时CPU空闲PID 1发起I/O占用1个tick的CPU，然后4-7tick保持准备就绪状态，8tick时PID 0完成I/O占用1个tick的CPU，在9tick时CPU空闲运行1个tick的CPU后完成。8tick时IOs空闲所以8-11tick进入阻塞状态，12tick时PID 1完成I/O，13tick时PID 1发起I/O进入阻塞状态5个tick后完成，在20tick时CPU空闲PID 1运行1个tick的CPU。CPU 9tick（45%）I/Os 16tick（80%）。
- Verified result / 验证结果:s1:CPU Busy 8 (53.33%) IO Busy  10 (66.67%) s2:CPU Busy 10 (62.50%) IO Busy  14 (87.50%) s3:CPU Busy 9 (50.00%) IO Busy  11 (61.11%)
- Analysis / 分析:
s1:系统先调度PID 0运行1个tick的CPU，然后发起I/O占用1个tick的CPU，PID 0进入阻塞状态5个tick。PID 1在1-2tick保持准备就绪状态，3-5tick因为PID 0在阻塞状态所以运行3个tick的CPU，然后在6tick完成。8tick的时候PID 0完成I/O占用1个tick的CPU，9tick发起I/O占用1个tick的CPU，PID 0进入阻塞状态5个tick，在15tick完成I/O占用1个tick的CPU。所以没有预测错误。
s2:错误的原因是我不知道IO设备可以多个一起运行，我一开始认为IO设备也只能1个tick里面只能运行一个，结果显示IO设备可以同时运行多个，就导致我的预测里tick的数量过多。所以预测错误。
s3:错误的原因也是我不知道IO设备可以多个一起运行，我一开始认为IO设备也只能1个tick里面只能运行一个，结果显示IO设备可以同时运行多个，就导致我的预测里tick的数量过多。所以预测错误。