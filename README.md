# Documentation

## Overview
* This engine consist of three elements given different classes, .object ,.board and .hollow.
    * .object 
        * the structure of 3d-object composed of difference classes. more precisely, this creats starting points or diresction for elements including .object itself.

    * .board
        * the smallest component of 3d object.

    * .hollow
        * complete the hole of .board.

## Limitaion
* some css-property is restricted. (property of .hollow is same as .board)
    * transform, transform~
    * width, height (.board)
    * margin (.board)
    * clip-path

* unless you understand about this engine well, you shouldn't use properties below.
    * background
    * ::before, ::after

* these properties are recommended.
    * grid or flex system
    * top, left (cannot use bottom or right)

## Variables
* creat a work by setting folllowing variables for elements.
    * .board, .hollow
        * --width
        * --height
        * --thick
        * --color
        * --side-color
        * --hole-width
        * --hole-height
        * --hole-top
        * --hole-left

    * common
        * --vertical