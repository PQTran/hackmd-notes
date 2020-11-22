# Web Development

###### tags: `frontend`

[ToC]

## Flexbox
[source](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)
### Background
Flexbox Layout intends to be a container for dynamic-sized items. 

#### Notes
- suits small-scaled layouts and components
  - consider grid layouts for large-scaled layouts
- container changes item properties in order to display
  - example properties: height, width, placement order
- flexible in layout direction
  - block layouts: vertical direction
  - inline layouts: horizontal direction

### Basics and Terminology
![flexbox diagram](https://i.imgur.com/BrIFMWO.png)

#### Terms

==flex container==: parent element
==flex items==: children elements
==main axis==: axis for flex items alignment
  ---   depends on flex-direction property (vertical; horizontal; etc)
==main-start==: start for flex items placement
==main-end==: end for     \" \" \"
==main size==: width or height of flex item based on flex-direction
==cross axis==: perpendicular axis of main axis
==cross-start== start for flex line
==cross-end==: end for \" \" \"
==cross size==: width or height of flex item based on (opp) flex-direction

### Container Properties
display:
```
enables flex context for all direct children
---
flex
inline-flex
```

flex-direction:
```
establishes single-direction main-axis
---
row; row-reverse
column; column-reverse
```

flex-wrap:
```
handles wrapping of children items
---
nowrap
wrap; wrap-reverse
```

flex-flow:
```
shorthand syntax for: flex-direction, flex-wrap
```

justify-content:
```
defines alignment along main axis
---
flex-start; flex-end; center
space-between; space-around; space-evenly
safe; unsafe
```

align-items:
```
defines placement along cross axis
---
flex-start; flex-end
center; stretch
safe; unsafe
```

align-content:
```
defines placement of lines for multiple line container (flex-wrap) 
---
flex-start; flex-end
center; stretch
space-between; space-around
```

### Item Properties
order:
```
flex item default order is the source order
---
integer (default: 0)
```

flex-grow:
```
specifies flex item grow proportions
---
integer (default: 0)
```

flex-shrink:
```
specifies flex item shrink proportions
---
integer (default: 1)
```

flex-basis:
```
specifies default size of element before container space is distributed
---
length; keyword (default: auto)
content
min-content; max-content; fit-content
```

flex:
```
recommended to use (intelligent handling of logic)
---
shorthand syntax for: flex-grow, flex-shrink (opt), flex-basis (opt)
default: 0 1 auto
```

align-self:
```
overrides alignment (container rule) for individual flex
```
