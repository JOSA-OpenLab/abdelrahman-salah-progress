# Week 08

## Task 1

I profiled the `cargo-bp show` workflow in the `battery-pack` project and found that it launched a separate `rustfmt` process for each generated Rust file. For the tested template, this meant 11 formatter processes.

I changed the implementation to batch all Rust files into one `rustfmt` invocation. The mean runtime decreased from **216.78 ms to 82.43 ms**, a **61.97% reduction**. Flame graphs and process tracing confirmed that repeated `rustfmt` startup was the main bottleneck. The optimized output matched the original output byte-for-byte, I opened an [issue](https://github.com/battery-pack-rs/battery-pack/issues/184) to suggest my fix.
