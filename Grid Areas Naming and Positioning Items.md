# Wiki-Grid Areas. Naming and Positioning Items

Created: June 30, 2021 2:55 PM
Created By: Liubov Kostomarova
Last Edited By: Liubov Kostomarova
Last Edited Time: June 30, 2021 3:05 PM

## Naming and Positioning Items by Grid Areas

Like grid line names, grid areas can also be named with the `grid-template-areas` property. Names can then be referenced to position grid items.

`grid-template-areas:   "header header"
                        "content sidebar"
                        "footer footer";grid-template-rows:    150px 1fr 100px;grid-template-columns: 1fr 200px;`

Sets of names should be surrounded in single or double quotes, and each name separated by a whitespace.

Each set of names defines a row, and each name defines a column.

![Wiki-Grid%20Areas%20Naming%20and%20Positioning%20Items%20d75b4ff422df499d9a40e51bbf979db6/Untitled.png](Wiki-Grid%20Areas%20Naming%20and%20Positioning%20Items%20d75b4ff422df499d9a40e51bbf979db6/Untitled.png)

`grid-row-start:    header;grid-row-end:      header;grid-column-start: header;grid-column-end:   header;`

Grid area names can be referenced by the same properties to position grid items: `grid-row-start`, `grid-row-end`, `grid-column-start`, and `grid-column-end`.

![Wiki-Grid%20Areas%20Naming%20and%20Positioning%20Items%20d75b4ff422df499d9a40e51bbf979db6/Untitled%201.png](Wiki-Grid%20Areas%20Naming%20and%20Positioning%20Items%20d75b4ff422df499d9a40e51bbf979db6/Untitled%201.png)

`grid-row:    footer;grid-column: footer;`

The `grid-row` and `grid-column` shorthand properties can also reference grid area names.

![Wiki-Grid%20Areas%20Naming%20and%20Positioning%20Items%20d75b4ff422df499d9a40e51bbf979db6/Untitled%202.png](Wiki-Grid%20Areas%20Naming%20and%20Positioning%20Items%20d75b4ff422df499d9a40e51bbf979db6/Untitled%202.png)

`grid-area: sidebar;`

The `grid-area` shorthand property can also be used to reference grid area names.

![Wiki-Grid%20Areas%20Naming%20and%20Positioning%20Items%20d75b4ff422df499d9a40e51bbf979db6/Untitled%203.png](Wiki-Grid%20Areas%20Naming%20and%20Positioning%20Items%20d75b4ff422df499d9a40e51bbf979db6/Untitled%203.png)

### Implicit Grid

An implicit grid is created when a grid needs to position items outside of the explicit grid because there isn’t enough space for items in the explicitly defined tracks or you decide to position something outside of the explicit grid. Those items are then auto-placed in the implicit grid.

The implicit grid can be defined using the `grid-auto-rows`, `grid-auto-columns`, and `grid-auto-flow` properties.

`grid-template-rows:    70px;`

`grid-template-columns: repeat(2, 1fr);`

`grid-auto-rows:        140px;`

In this example we’ve only defined one row track, therefore grid items 1 and 2 are `70px` tall.

A second row track was auto-created to make room for items 3 and 4. `grid-auto-rows` defines the row track sizes in the implicit grid, which is reflected by the the `140px` heights of items 3 and 4.

![Wiki-Grid%20Areas%20Naming%20and%20Positioning%20Items%20d75b4ff422df499d9a40e51bbf979db6/Untitled%204.png](Wiki-Grid%20Areas%20Naming%20and%20Positioning%20Items%20d75b4ff422df499d9a40e51bbf979db6/Untitled%204.png)

`grid-auto-flow: row`

The default flow (direction) of a grid is `row`.

![Wiki-Grid%20Areas%20Naming%20and%20Positioning%20Items%20d75b4ff422df499d9a40e51bbf979db6/Untitled%205.png](Wiki-Grid%20Areas%20Naming%20and%20Positioning%20Items%20d75b4ff422df499d9a40e51bbf979db6/Untitled%205.png)

`grid-auto-flow: column`

A grid’s flow can be changed to `column`.

![Wiki-Grid%20Areas%20Naming%20and%20Positioning%20Items%20d75b4ff422df499d9a40e51bbf979db6/Untitled%206.png](Wiki-Grid%20Areas%20Naming%20and%20Positioning%20Items%20d75b4ff422df499d9a40e51bbf979db6/Untitled%206.png)

`grid-template-columns: 30px 60px;grid-auto-flow:        column;grid-auto-columns:     1fr;`

In this example, we’ve only defined the sizes of the first two column tracks—item 1 is `30px` wide and item 2, `60px`.

Column tracks are auto-created in the implicit grid to make room for items 3, 4 and 5; and track sizes are defined by `grid-auto-columns`.

![Wiki-Grid%20Areas%20Naming%20and%20Positioning%20Items%20d75b4ff422df499d9a40e51bbf979db6/Untitled%207.png](Wiki-Grid%20Areas%20Naming%20and%20Positioning%20Items%20d75b4ff422df499d9a40e51bbf979db6/Untitled%207.png)

## **Implicitly Named Grid Areas**

Grid lines can generally be named whatever you’d like, but assigning names ending in -start and -end comes with added benefits—they implicitly create named grid areas, which can be referenced for positioning.

`grid-template-rows:    [outer-start] 1fr [inner-start] 1fr [inner-end] 1fr [outer-end];`

`grid-template-columns: [outer-start] 1fr [inner-start] 1fr [inner-end] 1fr [outer-end];`

In this example, both rows and columns have `inner-start` and `inner-end` lines, which implicitly assigns the grid area’s name as `inner`.

`grid-area: inner`

Grid items can then be positioned by the grid area name as opposed to line names.

![Wiki-Grid%20Areas%20Naming%20and%20Positioning%20Items%20d75b4ff422df499d9a40e51bbf979db6/Untitled%208.png](Wiki-Grid%20Areas%20Naming%20and%20Positioning%20Items%20d75b4ff422df499d9a40e51bbf979db6/Untitled%208.png)