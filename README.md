# AI Edition

> Examples of AI being impressive!

AI such as GitHub Copilot contribute greatly to a developer's work life but many of those moments are lost in time, only to live on in the good vibes.

This repository is just a small effort to record some of those moments.

The use-cases depicted by these moments are most likely undocumented officially (millions of possibilities), thus it might be useful for others to discover how AI can be used in programming.



## GitHub Copilot

### Convert list to a function that is similar to another one in context

https://github.com/user-attachments/assets/37b7e713-2edd-4068-962a-7edb76b26041

### Set default values

![time_savings](https://github.com/user-attachments/assets/a728c1f0-6eb1-4b29-b3ee-be0839b9be60)

### Library / package / module discovery and regular expression generation

In the midst of naturally leveraging GitHub Copilot, you can discover new libraries / tokens without having to leave your IDE.

For example, 

Prompt 1: Create a function to parse april.txt into 4 tokens

Code part of response:

```
def parse_april(lines):
    transactions = []
    for i in range(0, len(lines), 7):
        date = lines[i].strip()
        description = lines[i+2].strip() + " " + lines[i+3].strip()
        if lines[i+4].strip() == '-':
            amount = lines[i+5].strip()
            debit = False
        else:
            amount = lines[i+4].strip()
            debit = True
        transactions.append((date, description, amount, debit))
    return transactions
```

Prompt 2: Use a proper python parser not a for loop

Code part of response:

```
import re

def parse_april(text):
    pattern = re.compile(
        r'(\d{2}/\d{2}/\d{4})\n'  # Date 1
        r'(\d{2}/\d{2}/\d{4})\n'  # Date 2
        r'([^\n]+)\n'             # Description part 1
        r'([^\n]*)\n'             # Description part 2 (optional)
        r'(-|[\d,]+\.\d{2})\n'    # Amount or dash
        r'([\d,]+\.\d{2})'        # Amount
    )
    
    matches = pattern.findall(text)
    transactions = []
    
    for match in matches:
        date = match[0]
        description = match[2] + " " + match[3].strip()
        if match[4] == '-':
            amount = match[5]
            debit = False
        else:
            amount = match[4]
            debit = True
        transactions.append((date, description, amount, debit))
    
    return transactions
```

You can use "Explain This" to understand more about the ```re``` library.