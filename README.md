# pagexml-tools

[![GitHub Actions](https://github.com/knaw-huc/pagexml/workflows/tests/badge.svg)](https://github.com/knaw-huc/pagexml/actions)
[![Project Status: WIP – Initial development is in progress, but there has not yet been a stable, usable release suitable for the public.](https://www.repostatus.org/badges/latest/wip.svg)](https://www.repostatus.org/#wip)
[![Documentation Status](https://readthedocs.org/projects/pagexml/badge/?version=latest)](https://pagexml.readthedocs.io/en/latest/?badge=latest)
[![PyPI](https://img.shields.io/pypi/v/pagexml-tools)](https://pypi.org/project/pagexml-tools/)
[![PyPI - Python Version](https://img.shields.io/pypi/pyversions/pagexml-tools)](https://pypi.org/project/pagexml-tools/)

Utility functions for reading [PageXML](https://www.primaresearch.org/tools/PAGELibraries) files

## installing

### using poetry

```commandline
poetry add pagexml-tools
```

### using pip

```commandline
pip install pagexml-tools
```

## Using

PageXML-tools contains functions for parsing and for a range of analysis tasks.

### Parsing PageXML files and the Physical Document model

There is a tutorial that demonstrates the [physical document model API](./notebooks/Demo-understanding-the-document-model.ipynb)

PageXML-tools contains basic functionality for parsing a PageXML file that returns
a document model representing the content of the file. The HTR/OCR process that generates
PageXML, recognises text in an image of a physical document.

```python
from pagexml.parser import parse_pagexml_file

pagexml_file = "path/to/pagexml_file.xml"

page_doc = parse_pagexml_file(pagexml_file)

# a page document has an ID
print(page_doc.id)

# print descriptive statistics
print(page_doc.stats)

# iterative over text regions and lines
for tr in page_doc.text_regions:
    # a text_region has an ID and a bounding box derived from its coordinates
    print(tr.id, tr.coords.box)
    # a text_region can have sub-text_regions and lines
    for line in tr.lines:
        # a line has an ID, coordinates and text
        print(line.id, line.coords.box, line.text)
```

###

In addition to the basic parsing and handling of PageXML output, there is
functionality to support a range of tasks:

- checking the quality of the HTR/OCR process,
- classifying physical document types in a large set of PageXML documents,
- identifying sections in sequences of PageXML documents ([tutorial](./notebooks/Demo-analysing-pagexml-characteristics.ipynb#section_detection)),
- turning physical structure into logical structure,
- turning text lines into running text ([tutorial](./notebooks/Demo-from-lines-to-running-text.ipynb)),
- supporting different reading orders,
- reinterpreting and restructuring text regions and lines,

----

[USAGE](https://pagexml.readthedocs.io/en/latest/) |
[CONTRIBUTING](CONTRIBUTING.md) |
[LICENSE](LICENSE)
