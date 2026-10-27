Scripts are super useful, they can be used to automate geometry construction or plotting desired parameters and curves and such. In this example I want to take the effective index from multiple modes and plot them in the same figure.

**Functions**
[set](https://optics.ansys.com/hc/en-us/articles/360034928773-set-Script-command)
```
set("property",value);

This will set the properties of a currently selected object, including pull-downs and check boxes. It cannot be used to set the value of a selected object in a group.<br><br>Value can be a number or string. This function does not return any data.
```

**Commands**
Simulations can be ran through commands
```
findmodes
```

