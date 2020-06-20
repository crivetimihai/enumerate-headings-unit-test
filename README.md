Unit Testing
============

Serve the content
------------------

```bash
export VENV_DIR=~/.venv/enumerate-headings-unit-test
python3 -m venv ${VENV_DIR}
source ${VENV_DIR}/bin/activate
pip install --upgrade pip setuptools wheel
pip install -r requirements.txt
mkdocs serve
```

mkdocs.yaml
------------

- uses [awesome-pages](https://github.com/lukasgeiter/mkdocs-awesome-pages-plugin/) to generate `nav` from directory structure.
- Headings are generated automatically from `File-Name.md` => "File Name".

Example error
--------------

Occurs when:

- `01.Introduction/Empty-Page.md` is empty
- `01.Introduction/Missing-Heading-1.md` is midding a Heading 1. Note that
Heading 1 is generated automatically from the Title Page. Comment out the `enumerate-headings` plugins in `mkdocs.yaml` to see.


### Error

```
ERROR   -  Error building page '01.Introduction/Example-Page.md': can only concatenate str (not "NoneType") to str
Traceback (most recent call last):
  File "/home/cmihai/.venv/enumerate-headings-unit-test/bin/mkdocs", line 8, in <module>
    sys.exit(cli())
  File "/home/cmihai/.venv/enumerate-headings-unit-test/lib64/python3.7/site-packages/click/core.py", line 829, in __call__
    return self.main(*args, **kwargs)
  File "/home/cmihai/.venv/enumerate-headings-unit-test/lib64/python3.7/site-packages/click/core.py", line 782, in main
    rv = self.invoke(ctx)
  File "/home/cmihai/.venv/enumerate-headings-unit-test/lib64/python3.7/site-packages/click/core.py", line 1259, in invoke
    return _process_result(sub_ctx.command.invoke(sub_ctx))
  File "/home/cmihai/.venv/enumerate-headings-unit-test/lib64/python3.7/site-packages/click/core.py", line 1066, in invoke
    return ctx.invoke(self.callback, **ctx.params)
  File "/home/cmihai/.venv/enumerate-headings-unit-test/lib64/python3.7/site-packages/click/core.py", line 610, in invoke
    return callback(*args, **kwargs)
  File "/home/cmihai/.venv/enumerate-headings-unit-test/lib64/python3.7/site-packages/mkdocs/__main__.py", line 136, in serve_command
    **kwargs
  File "/home/cmihai/.venv/enumerate-headings-unit-test/lib64/python3.7/site-packages/mkdocs/commands/serve.py", line 141, in serve
    config = builder()
  File "/home/cmihai/.venv/enumerate-headings-unit-test/lib64/python3.7/site-packages/mkdocs/commands/serve.py", line 136, in builder
    build(config, live_server=live_server, dirty=dirty)
  File "/home/cmihai/.venv/enumerate-headings-unit-test/lib64/python3.7/site-packages/mkdocs/commands/build.py", line 292, in build
    _build_page(file.page, config, files, nav, env, dirty)
  File "/home/cmihai/.venv/enumerate-headings-unit-test/lib64/python3.7/site-packages/mkdocs/commands/build.py", line 214, in _build_page
    'post_page', output, page=page, config=config
  File "/home/cmihai/.venv/enumerate-headings-unit-test/lib64/python3.7/site-packages/mkdocs/plugins.py", line 94, in run_event
    result = method(item, **kwargs)
  File "/home/cmihai/.venv/enumerate-headings-unit-test/lib64/python3.7/site-packages/mkdocs_enumerate_headings_plugin/plugin.py", line 128, in on_post_page
    htmlpage.enumerate_toc(depth=self.config.get("toc_depth"))
  File "/home/cmihai/.venv/enumerate-headings-unit-test/lib64/python3.7/site-packages/mkdocs_enumerate_headings_plugin/html_page.py", line 33, in enumerate_toc
    if link.get("href") == heading.anchorlink and heading.depth <= depth:
  File "/home/cmihai/.venv/enumerate-headings-unit-test/lib64/python3.7/site-packages/mkdocs_enumerate_headings_plugin/heading.py", line 32, in anchorlink
    return "#" + self.heading.get("id")
TypeError: can only concatenate str (not "NoneType") to str
make: *** [Makefile:55: serve] Error 1
```
