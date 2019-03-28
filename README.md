# $ jinja2
A CLI interface to Jinja2
```
$ jinja2 helloworld.tmpl data.json --format=json
$ cat data.json | jinja2 helloworld.tmpl
$ curl -s http://httpbin.org/ip | jinja2 helloip.tmpl
$ curl -s http://httpbin.org/ip | jinja2 helloip.tmpl > helloip.html
```

## Install
`$ pip install jinja2-cli`

## Usage
```
Usage: jinja2 [options] <input template> [<input data> ..]

Options:
  --version             show program's version number and exit
  -h, --help            show this help message and exit
  --format=FORMAT       format of input variables: auto, env, ini, json,
                        querystring, yaml, yml
  -e EXTENSIONS, --extension=EXTENSIONS
                        extra jinja2 extensions to load
  -I INCLUDES, --includes=INCLUDES
                        extra jinja2 template directory to search for
                        (included) templates
  -D key=value          Define template variable in the form of key=value
  -s SECTION, --section=SECTION
                        Use only this section from the configuration
  --strict              Disallow undefined variables to be used within the
                        template
  -o FILE, --outfile=FILE
                        File to use for output. Default is stdout.
```

## Optional YAML support
If `PyYAML` is present, you can use YAML as an input data source.

`$ pip install jinja2-cli[yaml]`

## Optional TOML support
If `toml` is present, you can use TOML as an input data source.

`$ pip install jinja2-cli[toml]`

## Optional XML support
If `xmltodict` is present, you can use XML as an input data source.

`$ pip install jinja2-cli[xml]`

## Input data and overrides

Precedence of input sources and template variables
- Template variables defined with `-D`
- Rightmost input data
- ...  
- Leftmost input data

Input sources are merged left to right, meaning the dictionary is built by merging the data sources left to right using `dict.update()`.
This means that the input sources to the right take precedence, overriding values previous input sources, if there are parts of the dictionaries that overlap.

If no input data is given, standard input is read for input data.
If an <input data> is a single `-`, standard input is read as an input data.

## TODO
 * Variable inheritance and overrides
  * Tests!
