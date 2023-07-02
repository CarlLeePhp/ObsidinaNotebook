

### Lab 1

**Starter Template** Bootstrap 4.1.x

```html
<!doctype html>
<html lang="en">
  <head>
    <!-- Required meta tags -->
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">

    <!-- Bootstrap CSS -->
    <link rel="stylesheet" href="path/to/bootstrap/4.1.3/css/bootstrap.min.css">

    <title>Hello, world!</title>
  </head>
  <body>
    <h1>Hello, world!</h1>

    <!-- Optional JavaScript -->
    <!-- jQuery first, then Popper.js, then Bootstrap JS -->
    <script src="path/to/jquery-3.3.1.slim.min.js"></script>
    <script src="path/to/popper.js/1.14.3/umd/popper.min.js"></script>
    <script src="path/to/bootstrap/4.1.3/js/bootstrap.min.js"></script>
  </body>
</html>
```



### Lab 2 Basic Styles

#### Basic Typography Overview

The display styles are just bigger.

#### Typographic Utilities

.text-center .text-sm-left .text-md-right

.text-justify

.text-nowrap makes the text just go in one very long line.

#### Blockquotes and lists

.list-unstyled for ul makes it without bullets.

To have inline-lists, you need to add .list-inline for ul and .list-inline-item for li.

.blockquote .blockquote-footer

.blockquote-reverse makes it align right.

#### Bootstrap Colors

.gb-primary .text-white bg-faded

#### Work with Images

.img-fluid makes the pictures responsive.

.rounded .rounded-top

.rounded-circle



### Grid Layout

#### Containers and rows

.container & .container-fluid about 15px to the edge

#### Columns

.col .col-sm

You define any of those three things, a regular C-O-L, just to have them try to fit as many as possible, you can specify a breakpoint, and that will determine when the columns will go full horizontal, and then you can specify a number that will let you define how much of that grid that column should try to take up.

#### Multiple Columns

.col-sm-6 .col-md-4 .col-lg-3

####  Offset Column

.offset-sm-2

#### Nested Columns

.no-gutters removes the space in between the gutter.

So, anything that you can do with your grid, you can do in this new section, in this new row. And all you have to do is to insert a row inside an existing column, and you get a completely new 12-column grid to work with and then you can use whatever classes you want.



### Lab 4 Forms

#### 4-1

.form-group for the ancient element of input elements to get better space.

.form-control for input, select, textarea

.form-control-label for labels. It sets the form up for validation styles later on.

.form-text & .text-muted makes special style for the notice text for users.



#### 4-2 Check box & Radio

.form-check for the ancient of check or radio / .form-check-inline makes all check or radio with same name inline

.form-check-label for the label of check or radio

.form-check-input for the input of check or radio



#### 4-3

.sr-only is used to hide the label

.text-md-right is used to align text right for label

.col-form-label to vertically center labels with .form-controls

.form-group & row for each row



### Lab 5 Navigation

#### 5-1 Nav

.nav -> ul, .nav-item -> li, .nav-link -> a



#### 5-2 Navbar

Level 1: .navbar

Level 2: .navbar-nav

Level 3: .nav-item .nav-link



#### 5-3 Branding & Text

Using a element for navbar-brand

.navbar-text for text, will align right