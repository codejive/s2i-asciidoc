S2I Asciidoc Builder Image
=================

This is an S2I builder image that takes Asciidoc files from a source
repository, converts them into HTML using Asciidoctor and serves them up
using a simple HTTP server.

By default the builder looks for Asciidoc files in the `adoc` folder
in the source repository.

Usage
---------------------

For this to work you need to have S2I installed: https://github.com/openshift/source-to-image

```
s2i build https://github.com/quintesse/s2i-asciidoc.git --context-dir=test/adoc-sample/ quintesse/s2i-asciidoc adoc-sample
```

You can then run the resulting image via:

```
docker run -p 8080:8080 adoc-sample
```

Environment variables
---------------------

To set these environment variables, you can place them as a key value pair into a `.sti/environment`
file inside your source code repository.

* **ADOC_DIR**

    By default the builder looks in the `adoc` folder for any Asciidoc source files. This can be changed
    by setting this variable to the path where the builder _should_ look.

* **OUTPUT_DIR**

    By default all the output goes to `html`. This variable can be used to change that, although there
    really isn't much use for it.

* **ASCIIDOCTOR_OPTIONS**

    This variable can be used to pass any extra options to the `asciidoctor` command.

