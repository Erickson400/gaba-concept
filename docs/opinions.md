## A list of opinions, diciplines, and rants behind the project's design.

Is this a Language or a HLA? I have no clue.

Scopes {}, scopes everywhere!

Single command build system, no make files.

Package system like Odin. The user does not handle obj files, the linker, the fixer...etc. Running build on the main package directory is all you need to do.

Libraries are sub-packages of the main package, just copy and paste the folder and you're done.

No user defined macros. They're mostly made because the platform doesnt have the features the user desires, and they're hard to read for anyone other than the person who made it. Many of these features should be built into Gaba, with pseudo instructions, structs, built-in macros, and more. If a user wants a new macro, then it should be added to Gaba if it's actually useful, and not to fill a niche technique. I want to try not to bloat the ecosystem or overwhelm new users with endless macros, keep it simple. Built-in macros also have the advantage of using the full power of Odin instead of building a whole touring complete interpretor at comp-time. I might create an Odin library for doing codegen for power users, It'll have a Tokenizer, Parser, and AST just like the Odin's core packages by the same name. 



