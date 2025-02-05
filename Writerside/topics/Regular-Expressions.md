# Regular Expressions

Python’s `re` module provides tools for working with regular expressions, allowing pattern matching, searching, and text manipulation.

## Searching and matching text with regex

Example using `re.search()` to find the first match:

```python
import re

text = 'Email: example@email.com, Phone: 123-456-789'

email_match = re.search(r'\w+@\w+\.\w+', text)
phone_match = re.search(r'\d{3}-\d{3}-\d{3}', text)
numbers_match = re.search(r'\d', text)

print(email_match.group())
print(phone_match.group())
print(numbers_match.group())
```

```Plain Text
example@email.com
123-456-789
1
```

Example of `re.findall()` to find all matches:

```python
text = 'Email: example@email.com, Phone: 123-456-789'

emails = re.findall(r'\w+@\w+\.\w+', text)
phones = re.findall(r'\d{3}-\d{3}-\d{3}', text)
numbers = re.findall(r'\d', text)

print(emails)
print(phones)
print(numbers)
```

Output:

```python
['example@email.com']
['123-456-789']
['1', '2', '3', '4', '5', '6', '7', '8', '9']
```

## Replacing text with regex

Example of `re.sub()` to replace all matches with a text:

```python
text = 'Email: example@email.com, Phone: 123-456-789'  

replaced_text = re.sub(r'\d', '*', text)

print(replaced_text)
```

Output:

```Plain Text
Email: example@email.com, Phone: ***-***-***
```

## Advanced regex patterns and examples

Regular expressions support complex patterns with metacharacters and quantifiers:

- `^`: start of string
- `$`: end of string
- `.`: any character
- `\d`: digits
- `\s`: whitespace
- `\w`: alphanumeric
- `*`: 0+ times)
- `+`: 1+ times
- `?`: 0 or 1 time
- `{n}`:  exact n times

Example extracting valid URLs from text:

```python
pattern = r'https?://[a-zA-Z0-9.-]+(?:\.[a-zA-Z]{2,})+'

text = 'Visit https://example.com or http://site.org for info.'
urls = re.findall(pattern, text)

print(urls)
```

Output:

```python
['https://example.com', 'http://site.org']
```
