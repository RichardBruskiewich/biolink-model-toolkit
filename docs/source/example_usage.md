[![Python](https://img.shields.io/badge/python-3.7+-blue.svg)]()
[![PyPI](https://img.shields.io/pypi/v/bmt)](https://img.shields.io/pypi/v/bmt)

# Example Usage

BMT provides convenience methods to operate on the Biolink Model.

Using this toolkit you can,
- Get Biolink Model elements corresponding to a given Biolink class or slot name
- Get Biolink Model elements corresponding to a given external CURIE/IRI
- Get ancestors for a given Biolink Model element
- Get descendants for a given Biolink Model element
- Get parent for a given Biolink Model element
- Get children for a given Biolink Model element
- Check whether a given Biolink Model element is part of a specified subset


## Using the Toolkit class

The main entrypoint is the Toolkit class that provides various methods for accessing and working with the Biolink Model.

### Getting a Biolink Model element based on its name

```py
from bmt import Toolkit
t = Toolkit()
element = t.get_element('gene') # This returns the element for 'biolink:Gene'
```

### Get a Biolink Model element based on its mappings

```py
from bmt import Toolkit
t = Toolkit()
element_name = t.get_element_by_mapping('SEMMEDDB:CAUSES') # This returns 'causes'
element = t.get_element(element_name)

element_name = t.get_element_by_mapping('RO:0002410') # This returns 'causes'
element = t.get_element(element_name)
```

### Get ancestors for a given Biolink Model element

```py
from bmt import Toolkit
t = Toolkit()
ancestors = t.get_ancestors('gene')
```

The above returns a list of ancestors: `['gene', 'gene or gene product', 'macromolecular machine', 'genomic entity', 'molecular entity', 'biological entity', 'named thing']`

### Get descendants for a given Biolink Model element

```py
from bmt import Toolkit
t = Toolkit()
descendants = t.get_descendants('gene or gene product')
```

The above returns a list of descendants: `['gene', 'gene product', 'gene product isoform', 'RNA product', 'noncoding RNA product', 'microRNA', 'RNA product isoform', 'transcript', 'protein', 'protein isoform']`

### Check whether a given string is a valid Biolink Model category

```py
from bmt import Toolkit
t = Toolkit()
t.is_category('gene') # True
t.is_category('treats') # False
```

### Check whether a given string is a valid Biolink Model predicate

```py
from bmt import Toolkit
t = Toolkit()
t.is_predicate('related to') # True
t.is_predicate('interacts with') # True
t.is_predicate('disease') # False
```


## Using the Toolkit class with different versions of Biolink Model

BMT is pinned to a specific version of Biolink Model at each release. This can be configured to use your custom
version of Biolink Model YAML:

```py
from bmt import Toolkit
t = Toolkit('/path/to/biolink-model.yaml')
```

The path can be a file path or a URL.