<img src="assets/logo.png" width="112" height="112" alt="Blyx penguin fitting a short byte request inside whole storage blocks.">

# BlockSpan

Expand a byte request to whole storage blocks. This Blyx library is part of the collections and storage collection.

Merging requests saves seeks but can read unused gap bytes. Report each cost explicitly before changing a storage access pattern. [POSIX, pread and pwrite offsets](https://pubs.opengroup.org/onlinepubs/9799919799/functions/pread.html)

## Install and run

Install [Blyx 0.2.1](https://www.blyx-lang.space/download) with a Rust toolchain and host linker for native builds.

```sh
git clone --depth 1 --branch v0.1.0 https://github.com/Rahulchaube1/blyx-blockspan.git
cd blyx-blockspan
blyxc native-run example.blyx
blyxc native-run tests.blyx
```

[Run the editable browser example](https://www.blyx-lang.space/play?example=package-blockspan) · [Package page](https://www.blyx-lang.space/packages/blockspan) · [Handbook](https://doc.blyx-lang.space/guide/pelican)

## Import the module

Run this in the directory containing your application's entry file.

```sh
git clone --depth 1 --branch v0.1.0 https://github.com/Rahulchaube1/blyx-blockspan.git vendor/blockspan
```

```blyx
use vendor::blockspan::blockspan;

fn main() {
    let offset = 7.0;
    let length = 4.0;
    let block = 8.0;
    let result = blockspan_align(offset, length, block);
    if len(result) == 0 { println!("invalid"); return; }
    let mut i = 0;
    while i < len(result) {
        println!(at(result, i));
        i += 1;
    }
}
```

Expected output

```text
0
16
7
```

## API

`blockspan_align(offset, length, block)`

Returns [aligned start, bytes to read, requested start within read]. A zero-length request incurs zero reads. Counts must remain exactly representable. Invalid arguments and nonfinite results return an empty vector. Integers carried in numeric vectors use the exact range from −(2^53−1) to 2^53−1.

| Argument | Domain |
| --- | --- |
| offset | A nonnegative exact integer |
| length | A nonnegative exact integer |
| block | A positive exact integer |

## In use

[Pelican](https://github.com/Rahulchaube1/blyx-pelican) uses this module to compare per-request aligned I/O with coalesced unaligned reads for a sorted trace.

## Verification and contributions

The regression suite in [tests.blyx](tests.blyx) checks the example, boundary cases and invalid inputs. Include a short reproducer and your compiler version in [an issue](https://github.com/Rahulchaube1/blyx-blockspan/issues). The source is dual-licensed under [MIT](LICENSE-MIT) or [Apache-2.0](LICENSE-APACHE). Read the [artwork notice](assets/NOTICE.txt) for credits.

## Connect with Rahul Chaube

[Portfolio](https://www.rahulchaube1.com/) · [GitHub](https://github.com/Rahulchaube1) · [LinkedIn](https://www.linkedin.com/in/rahulchaube1) · [Hugging Face](https://huggingface.co/oncody) · [X](https://x.com/RahulChaube_) · [EverestQ](https://www.everestqai.com/) · [Contact](https://www.rahulchaube1.com/contact)

[Blyx website](https://www.blyx-lang.space/) · [BlyxTorch](https://www.blyx-lang.space/packages/blyxtorch) · [Handbook](https://doc.blyx-lang.space/) · [Community](https://www.blyx-lang.space/community)

Support Rahul’s open-source work through [GitHub Sponsors](https://github.com/sponsors/Rahulchaube1) or [Buy Me a Coffee](https://buymeacoffee.com/rahulchaube).
