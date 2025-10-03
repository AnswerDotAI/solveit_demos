## Nuggets of SolveIt

SolveIt is flexible! It combines the capabilities of an AI chat system (like Claude.ai or ChatGPT), of a notebook system (like Jupyter ), and of a hosted virtual private server.

This flexibility means you can use it for a lot. Here's some very short HOWTO examples, intended to be friendly for copy/pasting:

Here is how to...

## Basic interactions
### Install a private GitHub repo

To install private GitHub repos, you can call the installer in python and pass in a repo address which contains your GitHub token. token.

For examlpe, say you want to install the repo https://github.com/answerdotai/fastmigrate, where the GH user is `answerdotai` and the repo name is `fastmigrate`. 

``` python
import sys,subprocess,os
gh_token = os.getenv('GITHUB_TOKEN')
subprocess.run([sys.executable,'-m','pip','install','--force-reinstall',
                'git+https://{gh_token}@github.com/answerdotai/fastmigrate.git'])
```

### Export a SolveIt dialog as a gist in GitHub

To export a dialog into a GitHub gist, so you have a public or private URL you can share, click Settings (the gear), then "Notebook (.ipynb)" in the "Create Gist" row.

This requires that you previously configure a Setting for `GITHUB_TOKEN` from the dialog list.

### Export a SolveIt dialog's code as a Python module

To download a dialog as a Python module, click Settings (the gear), then the file name ending `.py` in the "Download File" row.

Only the code cells will be exported which you have tagged by selecting the bookmark icon, whose tooltip is "Will be exported?"

### Run a shell command

As with some notebook systems, you may run a command as a shell command (rather than a Python statement) by prefixing it with a `!`:

```
!ls # lists files in your instance's directory
```

### Launch a public web server

If you launch an HTTP server in your SolveIt instance which listens on port 8000, then it will be publicly reachable via HTTPS your instance's public domain name. That public URL is one visible next to the globe icon, in your instance list.

For instance, you can run a simple file server like so:

```sh
!python3 -m http.server
```

### Download a file

To download a file like `foo.md` directly from your instance, place it in the `static/` directory in your instance.

Then you can download it from `https://PRIVATE_INSTANCE_URL/static/foo.md`. (But beware: this does expose your **private** domain url, which grants access to the instance. If you want to share a file publicly, run a web server pointing at `static/`.)

### Upload a file, like an image

To upload a file to your instance, you can use the "Upload File" button on the dialog list page of your instance, or the Up arrow button at the top of your dialog.

### Add an image to the dialog

In a dialog, in a Note field, in addition to entering markdown, you may also add an image.

To add an image, copy it into your OS clipboard and then paste when you edit your note.

The note will be visible to the AI, so you can upload images for interpretation, handwritten notes for OCR, etc..

### Add a screenshot to the dialog

To add a screenshot to the dialog, hit CMD-SHIFT-S.

### Write in math in markdown using LaTeX

To enable SolveIt to render mathematical expression in LaTeX, in your own notes, in the AI's notes, or in output from evaluated code, set the following configurations in the instance Settings:

- `USE_KATEX=1`. Enables recognition of `\(...\)` for inline expressions, and of `\[...\]` and `$$...$$` for display expressions.

- `USE_KATEX=dollar`. Enables recognition of `\(...\)` or `$...$` for inline expressions, and of `\[...\]` and `$$...$$` for display expressions.


## Working directly with the AI

By default, the AI sees everything in the dialog above the current prompt you are entering.

But there are also ways to share information and tools directly with the AI. Here is how to...

### Share a variable value with the AI

To share the value of a Python variable with the AI, subit a Prompt to the AI and surround the variable you wish to share in dollar backtick notation.

For example, this saves a value into a Python variable.

```
import random
val = random.randint(1,10)
```

This Prompt passes that variable's value to the AI

```markdown
Please tell me the value of $\`val\`.
```

### Share a markdown file with the AI

Using the above mechanism, you can share markdown files, or other text files, directly to the AI by reading their contents as variable:

```python
contents = open('myfile.md').read()
```

Then in a prompt:

```
Please summarize me about $`contents`.
```

### Share a processed documentation with the AI

To share markdown files which teach the AI how to use software libraries, it helps to use libraries wich simplify web pages into clean markdown. The [contextkit](https://github.com/AnswerDotAI/contextkit) library helps for digesting many kinds of content into AI-friendly markdown, and the [contextpack](https://github.com/AnswerDotAI/contextpack) library has an index of documentation which is already pre-digested for AI consumption.

Loading predefined contexts with `contextpack`:

```python
from contextpack import *
claudette_docs = ctx_claudette.core_docs.get()
```

Reading a website other resources with `contextkit`:

```python
from contextkit import *
perplexity_docs = read_url("https://docs.perplexity.ai/api-reference/chat-completions")
```

Then you can teach the AI with a prompt as before:

```
Please familiarize yourself with claudette: $`claudette_docs`.
```

### Share a PDF file with the AI

Sharing a PDF is just a special case of sharing text, where you want to process the PDF file into markdown whcih it is easier for the AI to read.

`contextkit` provides helpers for downloading a PDF from arxiv and converting it to markdown, or downloading the latex if available:

```python
import contextkit
pdf_url = "https://arxiv.org/abs/2012.07805"
arxiv_dict = contextkit.read_arxiv(pdf_url,save_pdf=True)
text_md = contextkit.read_pdf('2503.15790.pdf')
text_latex = arxiv_dict.get('source','')
```

Then prompt based on the contents:

```
Please summarize this paper: $`text_md`
```

### Define and share a tool with AI

To define a tool for the AI, you simply expose a python function. So that the AI can understand what the function does, you should define it including parameter types and comments, using docments-style documentation.

```python
def reverse_string(s:str      # a string to reverse
                  ) -> str:   # reversed string
                  "Reverses a string"
                  return ''.join(reversed(list(s)))
```

Then you share it with the AI using ampersand backtick syntax:

```
Please familiarize yourself with the &`reverse_string` tool and use it to reverse "abcdefg".
```

### Use file access tools


TK.

## Using SolveIt AI

### Research a technical question

SolveIt has web search tools loaded by default. So you can use the SolveIt AI and the web search tools to support research into technical questions, such as how to select or use libraries to build a system.

TK.

### Study a mathematical topic

SolveIt can render LaTeX expressions, and you can use the SolveIt AI to teach you about mathematical topics. 

Try this prompt:

```
Please explain the attention mechanism to me. Show me the equation (using latex) and then explain the meaning of every term.
```

This requires configuring `USE_KATEX=1` (or `USE_KATEX=dollar` for even wider support).


### Do symbolic math (algebra, calculus, linear algebra, etc.)

If you configure `USE_KATEX=1` (or `USE_KATEX=dollar` for even wider support)

Solveit can also render mathematical expressions which are the output of code valuation, such as from libraries like `sympy`.

So you can render a symbolic expressions, like the quadratic equation:

```python
from sympy import *
(a,b,c,x,y,z) = symbols("a b c x y z")
f = a * x**2  + b * x + c
f
```

And you can compute and render the symbolic solution:

```python
solve(f,x)[0]
```


### Set up an agentic loop

TK.

### Perform Linux system administration

TK



