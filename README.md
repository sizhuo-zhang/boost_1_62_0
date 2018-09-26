Galois needs the `serialization` component of the `boost` library.
Here is how to cross compile `boost` to riscv.

1. Run `bootstrap.sh`.

        $ cd boost_1_62_0
        $ ./bootstrap.sh --prefix=`pwd`/build --with-libraries=serialization

2. Edit `project-config.jam`. Replace the line

        using gcc ;

    with

        using gcc : riscv : riscv64-unknown-linux-gnu-g++ ;

3. Compile using `b2`.
Option `link=static` only builds static library.
(We could use option `runtime-link=static` to force static link with C++ runtime library.
However, static link does not work well in Galois, so forget about it.)

        $ ./b2 link=static toolset=gcc-riscv install

