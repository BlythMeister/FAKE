# Convert Gherkin to HTML with Pickles

[*Pickles*](http://www.picklesdoc.com/) is a Living Documentation generator: it takes your Specification (written in Gherkin, with Markdown descriptions) 
and turns them into an always up-to-date documentation of the current state of your software - in a variety of formats.

To see the available Pickles APIs in FAKE, please see the [`API-Reference`](/reference/fake-tools-pickles.html) for the Pickles module.


## Minimal working example

```fsharp
#r "paket:
nuget Fake.Core.Target
nuget Fake.IO.FileSystem
nuget Fake.Tools.Pickles
//"

open Fake.Core
open Fake.IO.FileSystemOperators
open Fake.IO.Globbing
open Fake.Tools
open System.IO

let currentDirectory = Directory.GetCurrentDirectory()

Target.create "BuildDoc" (fun _ ->
    Pickles.convert (fun p ->
        { p with FeatureDirectory = currentDirectory </> "Specs"
                 OutputDirectory = currentDirectory </> "SpecDocs"
                 OutputFileFormat = Pickles.DocumentationFormat.DHTML })
)

Target.runOrDefault "BuildDoc"
```

