# YAML for clarion
Clarion classes for parsing and emitting YAML.  
Based on [LibYaml](https://github.com/yaml/libyaml) APIs.

### Examples
- import/export YAML data from/into Clarion GROUPs and QUEUEs.
```
  PROGRAM

  INCLUDE('yamlext.inc'), ONCE

  MAP
    INCLUDE('printf.inc'), ONCE

    Main()
  END

  CODE
  Main()
  
Main                                    PROCEDURE()
sFileName                                 STRING('.\data\array.yaml')

members                                   QUEUE
name                                        STRING(20)
                                          END

parser                                    TYamlParser
doc                                       TYamlDocumentProcessor
node                                      TYamlNode
i                                         LONG, AUTO

  CODE
  parser.Init()
  parser.SetInputFile(sFileName)
  IF NOT parser.Load(doc)
    MESSAGE(printf('Error loading %s: %s', sFileName, parser.ErrorDescription()))
    RETURN
  END
  
  !- load members queue from root sequence
  IF doc.RootNode(node)
    doc.ToSimpleQueue(node, members)
    
    !- test
    printd('=== ReadSimpleArray(%S) TEST ===', sFileName)
    LOOP i=1 TO RECORDS(members)
      GET(members, i)
      printd('members[%i].name: %s', i, members.name)
    END
    printd('=== END OF TEST ===')
  END
```
- a small utility to visualize YAML documents as a tree in a LIST control.
![YAML parser](https://github.com/mikeduglas/yaml-for-clarion/blob/master/screenshots/DocParser.jpg?raw=true)  

### Requirements
- C6.3 and higher
- ABC and Clarion template chains

### Dependencies
- [winapi](https://github.com/mikeduglas/winapi) (**latest version required**)
- [printf](https://github.com/mikeduglas/printf)

### Contacts
mikeduglas@yandex.ru

### Price
Negotiable  
[Buy now](https://www.clarionshop.com/checkout.cfm?pid=1709&q=1)
