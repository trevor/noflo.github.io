---
  title: "PacketsToString"
  library: "noflo-adapters"
  layout: "component"

---

```coffeescript
EXPORT=ARRAYIFY.IN:IN
EXPORT=JOIN.OUT:OUT
EXPORT=DELIMITER.IN:DELIMITER

Delimiter(Repeat) OUT -> IN MergeDelim(Merge)
',' -> IN MergeDelim() OUT -> DELIMITER Join(objects/Join)
Arrayify(adapters/PacketsToArray) OUT -> IN Join()

```