# Dee's Law For Hierarchical Database Storage

## Reference
  - Data needs to be referenced in a hierarchical manner.
  - A singular root element is unnecessary and is not maintained by this logic. 
  - Parents can have children.
  - Children can have only one parent.
  - Children can move between parents.
  - When a parent is moved its children move with it.
  - When a parent is removed its children traverse down the tree one level to the next logical parent.
  - When obtaining any record the obtainer should be presented with the level the record is at.
  - When obtaining a parent record the obtainer should be presented with the amount of children. 
  - When obtaining a "child" record the obtainer should be presented with the node path to the parent.
  - Data elements must maintain a unique id.
  - Data elements node path must also be human readable irrespective of of the id node path. 

## Minimum Standard Column Format
id (unique)  
name (unique)  
parent (id foreign key)  
node  
nodeName
level (integer)

## Test Cases
### FIND
-

### INSERT
- node, nodeName, and level records are maintained by the database and cannot be overridden
- records cannot be inserted with a non unique id
- records cannot be inserted with a parent that does not exist
- records should receive the correct node and nodeName path upon insertion
- if a child record was inserted the parent should be updated with the correct children count

### UPDATE 
- node, nodeName, and level records are maintained by the database and cannot be overridden
- records cannot be updated with a non unique id
- records cannot be updated with a parent that does not exist
- if a child record was moved:
  - the new parent should be updated with the correct children count
  - the previous parent should be updated with the correct children count
- children records should move with the parent, their node and nodeName paths in addition to the parent should be updated

### DELETE
- deleting a parent causes the children records to traverse down one level, their new parent should be updated with the correct children count
- if a child record was deleted the parent should be updated with the correct children count