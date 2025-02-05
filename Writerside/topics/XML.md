# XML

## Reading XML Files

The `xml.etree.ElementTree` module a built-in library for parsing, creating, and modifying XML data.

It represents XML as a tree structure where each element is a node.

To parse XML data use `.parse()`, then use `.find()` or `.findall()` to access its elements.

Base XML:

```xml
<items>
    <city id="1">
        <name>Madrid</name>
    </city>
    <city id="2">
        <name>Tokyo</name>
    </city>
</items>
```

Example of read:

```python
import xml.etree.ElementTree as ET

tree = ET.parse('data.xml')
root = tree.getroot()

for item in root.findall('city'):
    print(item.get('id'), item.find('name').text)
```

Output:

```Plain Text
1 Madrid
2 Tokyo
```

## Writing XML Files

You can create and save an XML document using `Element`, `SubElement`, and `ElementTree.write()`.

Example:

```python
root = ET.Element('items')
item = ET.SubElement(root, 'city', id='1')
ET.SubElement(item, 'name').text = 'Madrid'

tree = ET.ElementTree(root)
tree.write('output.xml')
```

## Editing XML

Modify XML content by updating element values and saving changes.

```python
for item in root.findall('city'):
    item.find('name').text = 'New City'

tree.write('updated.xml')
```

## Mapping XML to Classes

You can map XML data to Python objects using a simple class-based approach.

Example:

```python
class Item:
    def __init__(self, item_element):
        self.id = item_element.get('id')
        self.name = item_element.find('name').text

tree = ET.parse('data.xml')
root = tree.getroot()
items = [Item(item) for item in root.findall('city')]

for item in items:
    print(item.id, item.name)
```

Output:

```Plain Text
1 Madrid
2 Tokyo
```
