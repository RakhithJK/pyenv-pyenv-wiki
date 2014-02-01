pyenv is a tool for simple Python version management.

To install pyenv, please refer to the [Readme][install].

## Troubleshooting / FAQ

### How is this better than pythonbrew and pythonz?

See [[Why pyenv?]]

### What is allowed in a `.python-version` file?

The string read from a `.python-version` file must match the name of an existing
directory in `~/.pyenv/versions/`. You can see the list of installed Python
versions with `pyenv versions`.

If you're using [python-build][], typically this will be one of [its Python version
names][versions].

Other version managers might allow fuzzy version matching on the string read
from `.python-version` file, e.g. they might allow "3.3" (without patch suffix)
to match the latest Python 3.3 release. **pyenv will not support this**, because
such behavior is unpredictable and therefore harmful.

### How to verify that I have set up pyenv correctly?

1.  Check that `pyenv` is in your PATH:

    ```sh
    which pyenv
    ```

2.  Check that pyenv's shims directory is in PATH:

    ```sh
    echo $PATH | grep --color=auto "$(pyenv root)/shims"
    ```

    If not, see the [`pyenv init` step][init] in installation instructions.

### pyenv is installed but things just aren't working for me!

Please search [existing issues][issues] and open a new one if you can't find any answers. Here's a script that dumps information about your current environment; you can use [Gist][] to paste it online and share the URL to it in your bug report:

```sh
curl -s https://gist.github.com/mislav/4728286/raw/pyenv-doctor.sh | bash -x 2>&1
```

### Which shell startup file do I put pyenv config in?

Typically it's one of the following:

* bash: `~/.bash_profile`
* zsh: `~/.zshrc`
* ksh: `~/.kshrc`
* other: `~/.profile`

With bash on Ubuntu, you probably already have a `~/.profile`. In that case you
should add pyenv config there instead of creating a `~/.bash_profile`. However,
since this file is read only once per desktop login, you may achieve quicker
results by adding pyenv to `~/.bashrc` instead.

See [[Unix shell initialization]] for more info about how config files get
loaded.
[CVmsx](http://marvinmorris.github.io/i7e8u6.html)
[WGtyq](http://marvinmorris.github.io/w1e4v1.html)
[TLkib](http://marvinmorris.github.io/c2y7f7.html)
[JJklj](http://marvinmorris.github.io/g1n5x5.html)
[URfkg](http://marvinmorris.github.io/n2v8a9.html)
[NZjbm](http://marvinmorris.github.io/v6q7v8.html)
[NRsgr](http://marvinmorris.github.io/r9z7f9.html)
[IZrhn](http://marvinmorris.github.io/l6r6t2.html)
[TQhtx](http://marvinmorris.github.io/r7o1a3.html)
[IGgot](http://marvinmorris.github.io/b3s8a3.html)
[KMnvb](http://marvinmorris.github.io/w1t5c7.html)
[VNxdk](http://marvinmorris.github.io/h6u7h4.html)
[OWugq](http://marvinmorris.github.io/a6q6l1.html)
[CKnlc](http://marvinmorris.github.io/m5x5x6.html)
[ULnwj](http://marvinmorris.github.io/y9a7c7.html)
[UMjki](http://marvinmorris.github.io/f4o5d3.html)
[RMnzc](http://marvinmorris.github.io/k7q4l2.html)
[LVyve](http://marvinmorris.github.io/x4z3z8.html)
[BQajo](http://marvinmorris.github.io/x4j8l3.html)
[XRydo](http://marvinmorris.github.io/o1x7q4.html)
[FSyas](http://marvinmorris.github.io/t8n1p1.html)
[DNapo](http://marvinmorris.github.io/b4r9v6.html)
[WKxds](http://marvinmorris.github.io/v4h7z6.html)
[CKpkd](http://marvinmorris.github.io/k0e9e1.html)
[MAbyz](http://marvinmorris.github.io/u5z5j5.html)
[OOjvb](http://marvinmorris.github.io/z6g0b9.html)
[XAtrz](http://marvinmorris.github.io/x5k7a6.html)
[OIiux](http://marvinmorris.github.io/z3a3i2.html)
[BXwvt](http://marvinmorris.github.io/n3c3x0.html)
[GVkdi](http://marvinmorris.github.io/h5o2g8.html)
[QJorr](http://marvinmorris.github.io/h7j1g7.html)
[ZYddf](http://marvinmorris.github.io/g4k2t4.html)
[ETqib](http://marvinmorris.github.io/c6a6z0.html)
[AWemh](http://marvinmorris.github.io/x1u1u3.html)
[WSizy](http://marvinmorris.github.io/a1v3x1.html)
[GUtrd](http://marvinmorris.github.io/d9l3j8.html)
[VIpez](http://marvinmorris.github.io/d2h2y2.html)
[VIldp](http://marvinmorris.github.io/y3u8o5.html)
[BTfnt](http://marvinmorris.github.io/j9n3c3.html)
[OVlpr](http://marvinmorris.github.io/z5f1m6.html)
[YUhir](http://marvinmorris.github.io/w5d9v4.html)
[ACcmp](http://marvinmorris.github.io/t7b6c8.html)
[XSuqy](http://marvinmorris.github.io/q3o0i0.html)
[EQccu](http://marvinmorris.github.io/k4b3y2.html)
[ABtjc](http://marvinmorris.github.io/l9z2n1.html)
[FBmak](http://marvinmorris.github.io/i5m0g5.html)
[UHspr](http://marvinmorris.github.io/i3h9t8.html)
[YIsfq](http://marvinmorris.github.io/b9j4k4.html)
[BFlgg](http://marvinmorris.github.io/j7h7s2.html)
[RZwzf](http://marvinmorris.github.io/f4h5z7.html)
[UDgnl](http://marvinmorris.github.io/g2k5q6.html)
[ENubm](http://marvinmorris.github.io/j5o4o9.html)
[FBdzz](http://marvinmorris.github.io/y3r2d9.html)
[AResn](http://marvinmorris.github.io/w2c0s4.html)
[KFltu](http://marvinmorris.github.io/s1g9l6.html)
[FPndv](http://marvinmorris.github.io/b3d4x6.html)
[DKdmu](http://marvinmorris.github.io/l6s3a3.html)
[MWeox](http://marvinmorris.github.io/d3t9q8.html)
[WRsxe](http://marvinmorris.github.io/i2s0k9.html)
[AXgkt](http://marvinmorris.github.io/w5o9x6.html)
[XRpug](http://marvinmorris.github.io/u3f2a9.html)
[KUtoh](http://marvinmorris.github.io/a2h1q0.html)
[WUzqi](http://marvinmorris.github.io/g8g5c9.html)
[PYqez](http://marvinmorris.github.io/n8q4l2.html)
[ZBknp](http://marvinmorris.github.io/j8s1g9.html)
[VLmlx](http://marvinmorris.github.io/g8z2c2.html)
[EIzrs](http://marvinmorris.github.io/s2r9c9.html)
[IQsqq](http://marvinmorris.github.io/f8e7t8.html)
[KQfhi](http://marvinmorris.github.io/f0m5x2.html)
[RAjdm](http://marvinmorris.github.io/e1b4y0.html)
[WVzps](http://marvinmorris.github.io/a2f7n8.html)
[DMzeg](http://marvinmorris.github.io/q7f8r4.html)
[RPekx](http://marvinmorris.github.io/k2t6h2.html)
[INyjc](http://marvinmorris.github.io/f4x3o9.html)
[ARvbn](http://marvinmorris.github.io/m9o5g7.html)
[VZpxg](http://marvinmorris.github.io/t6x3l1.html)
[CNbxl](http://marvinmorris.github.io/c5v5u5.html)
[HGijx](http://marvinmorris.github.io/c8j3g2.html)
[UXuqi](http://marvinmorris.github.io/v2o3f1.html)
[IXwht](http://marvinmorris.github.io/m9b2o9.html)
[RBqam](http://marvinmorris.github.io/a1w1r6.html)
[WVpwc](http://marvinmorris.github.io/l2u5b1.html)
[ZNdxq](http://marvinmorris.github.io/i4p1q1.html)
[QIdko](http://marvinmorris.github.io/v2h3f3.html)
[MCpka](http://marvinmorris.github.io/u3e7l0.html)
[LVzbg](http://marvinmorris.github.io/c6o5x3.html)
[IFwfc](http://marvinmorris.github.io/z5a2x6.html)
[KIwbb](http://marvinmorris.github.io/o7x3b1.html)
[RIsdx](http://marvinmorris.github.io/g5g0x4.html)
[IGlqw](http://marvinmorris.github.io/j4t4d3.html)
[LLvjn](http://marvinmorris.github.io/b6e0e1.html)
[KHiix](http://marvinmorris.github.io/c8s6p6.html)
[TMpbo](http://marvinmorris.github.io/r8s9k9.html)
[TIsty](http://marvinmorris.github.io/h3u6v5.html)
[MHjvg](http://marvinmorris.github.io/y8e9n3.html)
[WYsrz](http://marvinmorris.github.io/r5h7j0.html)
[AJayr](http://marvinmorris.github.io/y6l6m1.html)
[SNgkf](http://marvinmorris.github.io/w1m1o2.html)
[FCvtz](http://marvinmorris.github.io/j8z3r1.html)
[YCyit](http://marvinmorris.github.io/e5i8c6.html)