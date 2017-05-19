# upd-configure

Generate `updfile.json` manifests for the `upd` utility

## Description

When updating a project using the `upd` utility, you need to provide a file
called `updfile.json` at the root of the project, called the manifest. Even
though you can write this file manually, this is inconvenient because it is
formatted with bare JSON and it does not allow dynamic choices based on the
environment. For example, on one platform you may want to compile C++ using
`gcc` while on another you may want to use `clang++`.

To alleviate this limitation you can write a script, in any language, that will
have the responsability to generate the `updfile.json` file the first time the
project is worked on. Generally this script is named `configure`, or in the
case of JavaScript, `configure.js`.

`upd-configure` provide utility functions to generate such a manifest file.

## Interface

### upd_configure.Manifest

This class represents a manifest being built.

    const manifest = new Manifest();

#### manifest.cli_template(binary_path, args)

* `binary_path`: `string` The name or the path of the command to run. If this
  is just name, then it'll be search for in the `$PATH`.
* `args`: `Array<ArgsPart>` The argument templates.
* Returns: an opaque object representing the template.

This creates a new command-line template in the manifest and returns a handle
to that template. That handle can be used in update rules.

#### manifest.source(pattern)

TODO

#### manifest.rule(cli_template, inputs, output_pattern, dependencies)

TODO

#### manifest.export(dirname)

* `dirname`: `string`: the path of the project's root directory.

This writes the manifest to the `updfile.json` file. `dirname` should generally
just be set to `__dirname` if your `configure.js` script is at the root of the
project.
