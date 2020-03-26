# Concurrency 并发与并行

| Recipe 专题 | Crates 库 | Categories 分类 |
|--------|--------|------------|
| [创建短期线程][ex-crossbeam-spawn] | [![crossbeam-badge]][crossbeam] | [![cat-concurrency-badge]][cat-concurrency] |
| [在两个线程之间传递数据][ex-crossbeam-spsc] | [![crossbeam-badge]][crossbeam] | [![cat-concurrency-badge]][cat-concurrency] |
| [维护全局可变状态][ex-global-mut-state] | [![lazy_static-badge]][lazy_static] | [![cat-rust-patterns-badge]][cat-rust-patterns] |
| [并发计算  *.iso 的 SHA1值][ex-threadpool-walk] | [![threadpool-badge]][threadpool] [![walkdir-badge]][walkdir] [![num_cpus-badge]][num_cpus] [![ring-badge]][ring] | [![cat-concurrency-badge]][cat-concurrency][![cat-filesystem-badge]][cat-filesystem] |
| [将分形计算工作分配到线程池][ex-threadpool-fractal] | [![threadpool-badge]][threadpool] [![num-badge]][num] [![num_cpus-badge]][num_cpus] [![image-badge]][image] | [![cat-concurrency-badge]][cat-concurrency][![cat-science-badge]][cat-science][![cat-rendering-badge]][cat-rendering] |
| [并行修改数组元素][ex-rayon-iter-mut] | [![rayon-badge]][rayon] | [![cat-concurrency-badge]][cat-concurrency] |
| [并行检测集合中的任何或所有元素是否匹配给定谓词][ex-rayon-any-all] | [![rayon-badge]][rayon] | [![cat-concurrency-badge]][cat-concurrency] |
| [使用给定谓词并行搜索项目][ex-rayon-parallel-search] | [![rayon-badge]][rayon] | [![cat-concurrency-badge]][cat-concurrency] |
| [并行排序 vector][ex-rayon-parallel-sort] | [![rayon-badge]][rayon] [![rand-badge]][rand] | [![cat-concurrency-badge]][cat-concurrency] |
| [并行 Map-reduce ][ex-rayon-map-reduce] | [![rayon-badge]][rayon] | [![cat-concurrency-badge]][cat-concurrency] |
| [并行生成 jpg 缩略图][ex-rayon-thumbnails] | [![rayon-badge]][rayon] [![glob-badge]][glob] [![image-badge]][image] | [![cat-concurrency-badge]][cat-concurrency][![cat-filesystem-badge]][cat-filesystem] |


[ex-crossbeam-spawn]: concurrency/threads.html#spawn-a-short-lived-thread
[ex-crossbeam-spsc]: concurrency/threads.html#pass-data-between-two-threads
[ex-global-mut-state]: concurrency/threads.html#maintain-global-mutable-state
[ex-threadpool-walk]: concurrency/threads.html#calculate-sha1-sum-of-iso-files-concurrently
[ex-threadpool-fractal]: concurrency/threads.html#draw-fractal-dispatching-work-to-a-thread-pool
[ex-rayon-iter-mut]: concurrency/parallel.html#mutate-the-elements-of-an-array-in-parallel
[ex-rayon-any-all]: concurrency/parallel.html#test-in-parallel-if-any-or-all-elements-of-a-collection-match-a-given-predicate
[ex-rayon-parallel-search]: concurrency/parallel.html#search-items-using-given-predicate-in-parallel
[ex-rayon-parallel-sort]: concurrency/parallel.html#sort-a-vector-in-parallel
[ex-rayon-map-reduce]: concurrency/parallel.html#map-reduce-in-parallel
[ex-rayon-thumbnails]: concurrency/parallel.html#generate-jpg-thumbnails-in-parallel

{{#include links.md}}
