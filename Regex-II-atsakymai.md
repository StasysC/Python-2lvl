#1
```python
def date_format(date):
    pattern = re.compile(r'^(\d{2})\.(\d{2})\.(\d{4})$')
    res = pattern.sub('\g<3> \g<2> \g<1>', date)
    return res
```

#2
```python
text = '''Workshop & Tutorial proposals: November 21, 2019
Notification of acceptance: December 1, 2019
Workshop & Tutorial websites online: December 18, 2019
Workshop papers: February 28, 2020
Workshop paper notifications: March 27, 2020
Workshop paper camera-ready versions: April 10, 2020
Tutorial material due (online): April 10, 2020'''

pattern = re.compile(r'[A-Z]\w+ \d{1,2}, 20\d{2}')
res = pattern.findall(text)
print(res)
```
#3
```python
pattern = re.compile(r'''
                        (^.+)                         # group 1
                        :\s
                        ([A-Z]\w+\s\d{1,2},\s20\d{2}) # group 2
                        ''', re.X | re.M)
seq = 1
for line in text.splitlines():
    res = pattern.search(line)
    print(f'{seq}.\nEvent: {res.group(1)}\nDate: {res.group(2)}\n')
    seq += 1
```
#4
```python
def censorhip(text, *args):
    pattern = re.compile(r'([a-ząčęėįšųūž])([a-ząčęėįšųūž]+)([a-ząčęėįšųūž])')
    for word in args:
        grouped = pattern.search(word)
        censored_part = len(grouped.group(2)) * '*'
        censored_word = pattern.sub(f'\g<1>{censored_part}\g<3>', word)
        text = text.replace(word, censored_word)
    print(text)
```
#5
```python
file = open('most_visited.html', 'r')
html = file.read()
domain_regex = re.compile(r'\w+\.\w+\.?\w*')
extracted_domains = domain_regex.findall(html)
print(extracted_domains)
```