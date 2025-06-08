# Overview

Write a utility called `ocat` which can `cat` a file containing a series of secrets made available via `export` eg lines in this syntax `export my-secret=12345678` and obscure the sensitive data eg outputting `export my-secret=1234<OBSCURED>`

**Example File syntax:**
```

export LLAMA_API_KEY=993

export AURA_INSTANCEID=6fc2
export AURA_INSTANCENAME=Insta1

export AAP2_PASSWORD="9b5bb6cfd"

```

**Desired output of `ocat ~/secrets/secret-env-vars.env`**

* include first 4 characters of the value
* Leave comment lines untouched

```
export LLAMA_API_KEY=993<OBSCURED>

export AURA_INSTANCEID=6fc2<OBSCURED>
export AURA_INSTANCENAME=Inst<OBSCURED>

export AAP2_PASSWORD="9b5b<OBSCURED>"
```

## Details

* Write the utility in bash
* By default outputs the contents of `~/secrets/secret-env-vars.env` 
* Output the result to STDOUT
* Under no circumstances modify the original file of exports
* Takes an optional command line argument of filename eg `ocat my-other-exports.env`
* ensure that secrets that are commented out are also obscured eg `# export my-old-key=12345678` becomes `# export my-old-key=1234<OBSCURED>
* Store the "obscuring string" `<OBSCURED>` as a env var
* ensure you accommodate different quoting syntaxes eg
  * `export my-old-key=12345678`
  * `export my-old-key="12345678"  # ie using double quotes`
  * `export my-old-key='12345678'  # ie using single quotes`
* If an export is less than 8 characters then obscure the entire export ie `export my-password=changeme` becomes `export my-password=<OBSCURED>`
* Create a simple README.md


