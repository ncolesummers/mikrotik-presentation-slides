## Mikrotik Configuration Generator



## What is a Mikrotik?
<img data-src="assets/mikrotikac2.jpg" alt="Mikrotik Router ac^2" width="66%">



## The Problem

Each router installed by our technicians was configured by hand.  This led to many routers having unique configurations, and misconfiguration was common.  The misconfigured routers generated support tickets, and the unique configurations increased the complexity of troubleshooting.




#### Additional Requirements
* The application needed to work offline
* Single Executable 



## Mikrotik Configuration Generator v1.0
The Python Console Program



#### TUI
<img data-src="assets/Mikrotik-Config-Gen-v1.0.png" alt="Screenshot of the console program">



#### Example function
```python
def input_validation(x) :
    '''This function substitutes characters that will break
    Mikrotik Scripting Syntax with their
    corresponding hex code.'''
    syntax_breakers = {
        '[': '\\5B',
        ']': '\\5C',
        '(': '\\28',
        ')': '\\29',
        '$': '\\$',
        '?': '\\?',
        '{': '\\7B',
        '}': '\\7D',
        ':': '\\3A',
        ';': '\\3B',
        '\\': '\\\\'
    }
    syntax_breakers_list = list(syntax_breakers.keys())
    for c in x :
        for key in syntax_breakers_list:
            if c == key:
                x = x.replace(c, syntax_breakers.get(c))
                syntax_breakers_list.remove(c)
    return x
```



#### Pain Points
* Lots of duplicated code, particularly in my string templates
* A TUI was easy for me to write, but difficult for our entry-level technicians to learn



## Journey to 2.0
Possible Solutions:
* Flutter Desktop - too new, still in alpha at the time
* Electron - memory footprint was too high for the target laptops
* Winforms - well-documented and supported native solution 
* Fyne - The GUI library written in Go with the most stars on Github



#### Winforms and C#
* Winforms made building a GUI simple
* I used the DotLiquid library for templating



#### GUI