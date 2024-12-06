This is a reproduction of 2 bugs related to features and building.

I used workspaces because the bug cannot be reproduces with only crate folders

Crate1 has a compile error on purpose.

Crate2 includes crate1 as a dependency based on its `feature1` feature.

Crate3 include Crate2 without features. Dev dependencies add `feature1` to the crate2 features

Crate4 include Crate1-1 with no default features.


## Issue 1

When going inside `crate3` and running the following command, we get a compile error
``` bash
    cargo build --release
```

Because we are building the release, the dev dependencies shouldn't influence the compilation result
We expect crate3 to compile correctly, because crate2 compiles correctly when no features are activated

## Issue 2

When going inside `crate4` and running the following command, we get a compile error
``` bash
    cargo build --release
```

Because we use the `default-features` flag for the crate1-1 dependency inside the crate4 Cargo.toml, we expect crate1-1 to compile correctly. This is not the case

