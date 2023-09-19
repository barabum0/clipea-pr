# Clipea 📎🟢

[![Install with Homebrew](https://img.shields.io/badge/Homebrew-Tap-blue.svg)](https://github.com/dave1010/homebrew-clipea)

**Like Clippy but for the CLI. A blazing fast AI helper for your command line.**

Clipea is a barebones, cheaper and hackable [Copilot for CLI](https://githubnext.com/projects/copilot-cli).

It has similar roots to [Hubcap](https://github.com/dave1010/hubcap) but is less dangerous and actually designed to be a usable productivity tool, rather than just a tech demo.

Tell Clipea what you want to do and it'll give you a shell command, asking you if you want to run it. Clipea works even better with Zsh, as it adds the shell command to your console as a pending command, just as if you had typed it yourself!

> [!WARNING]
> AI isn't perfect. Clipea might suggest a dangerous command. Be careful.

## Quick start

    brew tap dave1010/clipea
    brew install clipea
    clipea setup
    clipea alias

## Usage

### Without the Zsh shell integration

    clipea convert test.mp4 to a gif

Type `y<enter>` to run the command. Anything else or `<ctrl-c>` to cancel.

### With the Zsh shell integration (Recommended)

    ?? how many gig free do i have

Type `<enter>` to run the command. The command is editable in your shell buffer, ready to run, so you can do
usual things like `<ctrl-c>` to cancel or `<ctrl-a>` to go to the start of the line

### More examples

    ?? count loc recursively
    ?? open my shell login script in my editor
    ?? git fetch, rebase master, safely force push
    ?? open bbc news
    ?? check the spf record for example.com
    ?? What port is my webserver listening on
    ?? Where is nginx writing logs
    ?? Rename all txt files space to underscore
    ?? Install something that converts pdf to text
    ?? Find files bigger than 10mb
    ?? Check cors headers for api.example.com
    ?? Make a 30 char password 
    ?? Quick http server
    ?? Highlight URLs in index.html
    ?? Extract package.tar.gz
    ?? Show me just the headings from README.md
    ?? Find replace all PHP files in project that call eval function with safe_eval
    ?? Convert file.avi to gif

### Advanced usage and tips

GPT-4 mode: just start the query with a "4". Remember that OpenAI charge lots more for GPT-4.
Generally the standard GPT-3.5 is fine for commandline stuff.

    ?? 4 create a text file explaining quantum mechanics in a haiku in the style of a pirate

You can also send in data via stdin. Clipea limits you to 8192 bytes, so the LLM isn't overwhelmed.

    ls -F | ?? explain this project setup

Generally it's best to give Clipea a filename to create a commnand for, rather than the actual file contents.

    ?? count how many packages are in package.json

Clipea gets given some environment limited information like your OS, shell and path.
This allows it to give better responses.

    ?? wheres my shell config
    ?? install curl
    ?? compare README.md to my clipboard

### Feedback and editing

Just use your shell history by pressing the `<up>` arrow key. Your cursor will be at the end of
the last line, ready to edit it.

For example: typing `?? list js files recursively` may give
    
    $ find . -name "*.js"

Then to edit, press `<up>` then ` ignore node modules` to get something like

    $ find . -name "*.js" -not -path "./node_modules/*"

## 🚀 Installation and setup

### Mac

[![Install with Homebrew](https://img.shields.io/badge/Homebrew-Tap-blue.svg)](https://github.com/dave1010/homebrew-clipea)

    brew tap dave1010/clipea
    brew install clipea
    clipea setup

### Manual install

    pip install llm
    git clone https://github.com/dave1010/clipea.git
    cd clipea
    ./clipea setup
    ./clipea add current dir to my path on shell login

### Zsh Shell integration and Alias

> [!NOTICE]
> The `??` shell alias is highly recommended if you use zsh

Clipea can set up a very handy `??` alias.
As well as being quicker to type,
this uses zsh's `print -z`, allowing it to output commands on the commandline.

Install the alias:

    clipea alias

## Internals

Clipea is currently written in PHP but may switch to Python ([#3](https://github.com/dave1010/clipea/issues/3)).

Clipea uses [llm](https://github.com/simonw/llm) to interact with large language models.

By default it will use OpenAI's GPT-3.5 model but can be configured to other models, such as Llama.
Running `clipea setup` will talk you through getting OpenAI keys.

## Warnings

### Safety

AI isn't perfect. Clipea might suggest a dangerous command. Be careful.

Always read and check what Clipea suggets before accepting it.

### Privacy

Clipea uses OpenAI's APIs by default, though can be set to use any LLM that `llm` supports.

Only very basic environment info like your OS and editor is sent to the LLM.

Run `clipea env` to see the data the LLM gets.

### Cost

As a very rough example, using the default GPT-3.5, 100 Clipea queries to OpenAI cost $0.02.
Set a quota and keep an eye on costs to make sure.

## Contributing

Contributions welcome.

## Licence

MIT License

Copyright (c) 2023 Dave Hulbert