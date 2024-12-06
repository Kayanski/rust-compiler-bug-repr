This is a reproduction of a bug related to features and building.

I used workspaces because the bug cannot be reproduces with only crate folders

Crate1 has a compile error on purpose.

Crate2 includes crate1 as a dependency based on its `feature1` feature.

Crate3 and Crate4 both include Crate2 without features.

Crate3 include Crate2 with the `feature1` feature only inside dev-dependencies.




When going inside `crate3` and running the following command, we get a compile error
``` bash
    cargo build --release
```

When going inside `crate4` and running the following command, it compiles without an issue
``` bash
    cargo build --release
```

## Expected behavior

Because we are building the release, the dev dependencies shouldn't influence the compilation result
We expect crate3 to compile correctly