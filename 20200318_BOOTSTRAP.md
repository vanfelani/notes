# Bootstrap

Bootstrap is an open source toolkit for developing with HTML, CSS, and JS. You can download it or use a CDN.

## BootstrapCDN
When you only need to include Bootstrap’s compiled CSS or JS, you can use BootstrapCDN.  

A content delivery network (CDN) refers to a geographically distributed group of servers which work together to provide fast delivery of Internet content.  

**CSS only**
```html
<link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.4.1/css/bootstrap.min.css">
```
**JS, Popper.js, and jQuery**
```html
<script src="https://code.jquery.com/jquery-3.4.1.slim.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/popper.js@1.16.0/dist/umd/popper.min.js"></script>
<script src="https://stackpath.bootstrapcdn.com/bootstrap/4.4.1/js/bootstrap.min.js"></script>
```

## Container
Bootstrap comes with three different containers:

- `.container`, which sets a max-width at each responsive breakpoint
- `.container-fluid`, which is `width: 100%` at all breakpoints
- `.container-{breakpoint}`, which is `width: 100%` until the specified breakpoint
```html
<main class="container"></main>
```
| | Extra small <576px | Small ≥576px | Medium ≥768px | Large ≥992px | Extra large ≥1200px |
|---|---|---|---|---|---|
| .container | 100% | 540px | 720px | 960px | 1140px |
| .container-sm | 100% | 540px | 720px | 960px | 1140px |
| .container-md | 100% | 100% | 720px | 960px | 1140px |
| .container-lg | 100% | 100% | 100% | 960px | 1140px |
| .container-xl | 100% | 100% | 100% | 100% | 1140px |
| .container-fluid | 100% | 100% | 100% | 100% | 100% |

## Navigation
Navbars come with built-in support for a handful of sub-components. Choose from the following as needed:

- `.navbar-brand` for your company, product, or project name.  
- `.navbar-nav` for a full-height and lightweight navigation (including support for dropdowns).  
- `.navbar-toggler` for use with our collapse plugin and other navigation toggling behaviors.  
- `.form-inline` for any form controls and actions.  
.navbar-text for adding vertically centered strings of text.  
- `.collapse.navbar-collapse` for grouping and hiding navbar contents by a parent breakpoint.
```html
<nav class="navbar navbar-expand-lg navbar-light bg-light">
    <a class="navbar-brand" href="./index.html">Web Application</a>
    <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarNav">
        <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" id="navbarNav">
        <ul class="navbar-nav">
            <li class="nav-item active">
                <a class="nav-link" href="./index.html">Home</a>
            </li>
            <li class="nav-item">
                <a class="nav-link" href="./items/index.html">Items</a>
            </li>
        </ul>
    </div>
</nav>
```

## Table
Table styles:
- `.table` - base table style
- `.table-dark` - invert table color
- `.thead-{light|dark}` - change table header color
- `.table-striped` - add zebra-striping to table rows within the tbody
- `.table-bordered` - add borders on all sides of the table and cells
- `.table-borderless` - remove all borders on a table
- `.table-hover` - enable hover state on table rows within a tbody
- `.table-sm` - cut cells padding in half
```html
<table class="table table-striped table-bordered table-hover"></table>
```
Other table library: [DataTables](https://datatables.net/)

## Button
Button styles:
- `primary` - blue
- `secondary` - gray
- `success` - green
- `danger` - red
- `warning` - yellow
- `info` - tosca
- `light` - white
- `dark` - black
- `link` - transparent

Add `outline-` before default styles to remove background colors.

Button size:
- `.btn-lg` - larger buttons
- `.btn-sm` - smaller buttons
- `.btn-block` - block level buttons (full parent width)

```html
<a class="btn btn-secondary" href="index.html" role="button">Back</a>

<button type="submit" class="btn btn-primary">Save</button>
```

## Spacing
The classes are named using the format `{property}{sides}-{size}` for xs and `{property}{sides}-{breakpoint}-{size}` for sm, md, lg, and xl.

Where property is one of:

- `m` - set margin  
- `p` - set padding  

Where sides is one of:

- `t` - set top  
- `b` - set bottom  
- `l` - set left  
- `r` - set right  
- `x` - set both left and right  
- `y` - set both top and bottom  
- `blank` - set all 4 sides 

Where size is one of:

- `0` - set the margin or padding to 0  
- `1` - set the margin or padding to $spacer * .25  
- `2` - set the margin or padding to $spacer * .5  
- `3` - set the margin or padding to $spacer  
- `4` - set the margin or padding to $spacer * 1.5  
- `5` - set the margin or padding to $spacer * 3  
- `auto` - set the margin to auto

## Form
Form styles:
- `.form-control` - general style for `<input>`s, `<select>`s, and `<textarea>`s
- `.form-control-file` - general style for file inputs
- `.form-control-plaintext` - style readonly and disabled input as plain text

Other combobox library: [Select2](https://select2.org/)

Layout:
- `.form-group` - group labels, controls, optional help text, and validation message
- `.row`, `.form-row`, `col-*` - layout form using grid classes
- `.col-form-label` - center labels with their associated form controls
- `.form-inline` - display labels, controls, and buttons on a single horizontal row

Help & validation:
- `.form-text` - display small help text
- `.is-valid` - indicate a field is valid
- `.is-invalid` - indicate a field is invalid
- `.valid-feedback` - style text displayed on valid input
- `.invalid-feedback` - style text displayed on invalid input

```html
<form method="POST">
    <div class="form-group">
        <label for="id">Id</label>
        <input class="form-control-plaintext" name="id" id="id" disabled />
    </div>
    <div class="form-group">
        <label for="amount">Amount</label>
        <input class="form-control" name="amount" id="amount" />
    </div>
</form>
```

## Breadcrumb
```html
<nav aria-label="breadcrumb">
    <ol class="breadcrumb">
        <li class="breadcrumb-item active" aria-current="page">Home</li>
    </ol>
</nav>
```

## How to Set Favicon
Put favicon.ico file in project root