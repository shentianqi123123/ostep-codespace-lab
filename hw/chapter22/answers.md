# Q1
使用 -s 0 -n 10 -C 3，FIFO 命中 1 次，LRU 命中 2 次，OPT 命中 4 次。使用 -s 0 -n 10 -C 3，FIFO 命中 2 次，LRU 命中 2 次，OPT 命中 3 次。使用 -s 0 -n 10 -C 3，FIFO 命中 4 次，LRU 命中 4 次，OPT 命中 4 次。OPT 效果最好。

# Q2
缓存大小只需增加 1（变为 6），FIFO 和 LRU 就能达到 18 次命中，与 OPT 相同。

# Q3
RAND, FIFO, LRU 的命中率几乎一样。只有 OPT 有很高的命中率。

# Q4
LRU 比 RAND 高约8个百分点：2位 CLOCK 接近 LRU。真实程序只需很少页：共254页，32页就能达到99.8%。在有局部性的情况下，LRU 比 RAND 表现提升约8%。CLOCK 算法如果只给 1 个 bit，表现像 FIFO；如果给 2 个 bit，它的表现就非常接近 LRU。

# Q5
只需要非常小的缓存 32 * 4KB = 128KB，就能满足 99.8% 的请求。