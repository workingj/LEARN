# Bootstrap

- [x] [Cheat Sheet](https://hackerthemes.com/bootstrap-cheatsheet/)

[Introduction to Bootstrap](https://getbootstrap.com/docs/4.1/getting-started/introduction/)

- There are a few required links to use Bootstrap (the CSS file and two <meta> tags)
- Bootstrap 4 has a grid system implemented using flexbox
- The grid system is made of containers, rows, and columns that work together to make a web page’s layout.
- Containers are needed to implement the grid.
- Containers hold rows which hold columns.
- Bootstrap’s grid follows a 12 column system.
- Bootstrap uses responsive design and is built around breakpoints related to device screen sizes.
- To manually set the width of a column we have to follow Bootstrap’s naming convention.
- We can add multiple classes to a column to determine how wide a column should be on specific breakpoints

## Grid Layout

- Max Width 12 Cols a `col-#`
- `col-auto` depends on the elemnts content size

## Breakpoints

[Grid Options](https://getbootstrap.com/docs/4.2/layout/grid/#grid-options)

| Category    | short      | Breakpoint Range |           Device Type |
| :---------- | ---------- | ---------------- | --------------------: |
| Extra smal  | `col-#`    | < 576 px         |  portrait smartphones |
| Small       | `col-sm-#` | ≥ 576 px         | landscape smartphones |
| Medium      | `col-md-#` | ≥ 768 px         |               tablets |
| Large       | `col-lg-#` | ≥ 992 px         |              desktops |
| Extra Large | `col-xl-#` | ≥ 1200 px        |         large desktop |

**Breakpoint Naming Convention**

* `"col-{breakpoint}-{width}"`
* `{breakpoint}` can be `sm`, `md`, `lg`, or `xl`
* `{width}` can be set from `1` to `12`

