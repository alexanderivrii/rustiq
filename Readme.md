[![Rust](https://github.com/smartiel/rustiq/actions/workflows/rust.yml/badge.svg?branch=main)](https://github.com/smartiel/rustiq/actions/workflows/rust.yml)

# Rustiq: A quantum circuit compiler in Rust

This library contains implementations of various quantum synthesis algorithms.
It can handle:
 - Graph state synthesis
 - Synthesis of codiagonalization circuits for sets of commuting Pauli operators
 - Pauli network synthesis (i.e. synthesis of sequences of Pauli rotations)



## Python library

All the synthesis methods are binded in python and the repo can be installed via pip:

```bash
pip install . 
```

You might need to install rust!

## Building the project (Rust)


```bash
cargo build --release
```


## Running the synthesis algorithm

### In python

See the `examples` folder for examples of python usage (the file names are pretty self-explainatory)

### Using the command line tool (for Pauli network only)

The directory `benchmarks/chem/` contains text files describing set of Pauli operators used in UCCSD Ansätze.
The file names are pretty straightforward to parse.

Once the crate is compiled, you can run the synthesizer as follows:

```bash
./target/release/rustiq <FILENAME> 
```

By default, the program prints the output circuit. You can simply ask the program for the running time, the CNOT count, and the CNOT depth
by adding the flag `--onlyinfo` (the circuits might be huge).

```bash
./target/release/rustiq <FILENAME> --onlyinfo
```

You can switch between the count and depth minimizing algorithms via the `--metric` option:

```bash
./target/release/rustiq <FILENAME> --onlyinfo --metric=depth
```

or

```bash
./target/release/rustiq <FILENAME> --onlyinfo --metric=count
```

Finally, you can ask the compiler to preserve the operator ordering (up to allowed commutations) using `--keeporder` flag:

```bash
./target/release/rustiq <FILENAME> --keeporder
```