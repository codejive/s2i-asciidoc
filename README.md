S2I Asciidoc Builder Image
=================

This is an S2I builder image that takes Asciidoc files from a source
repository, converts them into HTML using Asciidoctor and serves them up
using a simple HTTP server.

By default the builder looks for Asciidoc files in the `adoc` folder
in the source repository.

Usage
---------------------

_IMPORTANT: for this to work you need to have S2I installed: https://github.com/openshift/source-to-image_

If you just want a very quick simple example, try this:

```
s2i build https://github.com/quintesse/s2i-asciidoc.git --context-dir=test/adoc-sample/ quintesse/s2i-asciidoc adoc-sample-image
```

This will look for any Asciidoc files in the `adoc` folder in the repository https://github.com/quintesse/s2i-asciidoc/tree/master/test/adoc-sample
and convert all of it to HTML. It will then generate a local Docker image called `adoc-sample-image` containing all that HTML and an HTTP server.

You can then run the resulting image via:

```
docker run -p 8080:8080 adoc-sample-image
```

Which will make the generated HTML available in your browser at:

http://localhost:8080

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

OpenShift Manual Setup
---------------------

If you want to use the S2I Asciidoc builder image properly in an OpenShift v3 server then follow these steps in the web console:

 - Log in to the OpenShift console
 - Select or create a project
 - Click the "Add to Project" button
 - Select the "Import YAML / JSON" tab
 - Copy & paste the contents of the [image-streams.json](https://github.com/quintesse/s2i-asciidoc/blob/master/image-streams.json) file into the text box
 - Click the "Create" button

Now whenever you go back to the "Add to Project" screen there should be an entry for the "Asciidoc Builder".


