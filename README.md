# 3D Room CSS (`room-2.0.0.css`)

> [!NOTE]
> Currently, `room-3.0.0.css` is in production.



A pure CSS library that uses CSS variables and transforms to create 3D rooms and models. This allows you to build complex 3D scenes using only HTML and CSS.

## Features

- **Pure CSS:** No JavaScript required.
- **Customizable:** Easily customize dimensions, colors, and other properties using CSS variables.
- **3D Transforms:** Utilizes `preserve-3d` and 3D transform functions to create depth and perspective.
- **Component-based:** Build complex objects by combining simple elements (`.board`, `.base`, `.hollow`).
- **Flexible:** Objects can be nested and positioned within 3D space.

## Usage

> [!IMPORTANT]
> It is recommended to use the latest version of Google Chrome for the best experience.



1.  **Include the CSS file:**
    ```html
    <link rel="stylesheet" href="https://pinattutaro.github.io/room/room.css">
    ```

2.  **Create the HTML structure:**
    The basic structure consists of a main container with the `.room` class that holds all 3D objects. Place `.object` elements inside the room.

    ```html
    <div class="room">
        <div class="object">
            <!-- Add 3D components here -->
        </div>
    </div>
    ```

3.  **Build objects:**
    Use the `.board`, `.base`, and `.hollow` classes to construct 3D shapes. Their appearance and position are controlled by CSS variables set via inline styles.

    - **`.board` / `.base`:** Create cuboids ("boards").
    - **`.hollow`:** Create hollows or holes inside boards.
    - **`.object`:** Container for placing and grouping other components. `.object` itself handles positioning in 3D space, while its inner elements can be arranged using standard CSS layout properties like `display: grid` or `display: flex`.

      **Example (from `sample/sam1.html`):**
      The shower room wall tiles in `sample/sam1.html` use `display: grid` on an `.object` to arrange tiles.

      ```html
      <div class="object right shower-tile" ...>
          <div class="board"></div>
          <div class="board"></div>
          ...
      </div>
      ```

      ```css
      .shower-tile {
          display: grid;
          grid-template-columns: repeat(15, 1fr);
          grid-template-rows: repeat(7, 1fr);
          place-items: center;
      }
      ```

### Positioning with .left and .right

To easily orient objects to the sides of the room, you can use the `.left` and `.right` helper classes on an `.object` container. These classes apply a `transform` to rotate the object and its contents to face the left or right wall of the 3D scene.

- **`.left`**: Orients the object to face the left side.
- **`.right`**: Orients the object to face the right side.

This is useful for placing items like windows or decorations on walls. Any properties of the child elements, such as holes created with `--hole-*` variables, will be correctly oriented along with the parent object.

**Example:**
```html
<div class="room">
    <!-- This object will be on the left wall -->
    <div class="object left">
        <div class="board" style="--hole-width: 50px; --hole-height: 50px;"></div>
    </div>
</div>
```

4.  **Customize with CSS variables:**
    Override default variables or define your own to control the scene. Main variables for shaping objects are:
    - `--width`: Width of the element.
    - `--height`: Height of the element.
    - `--thick`: Thickness (depth) of the element.
    - `--color`: Main face color.
    - `--side-color`: Side face color.
    - `--vertical`: Vertical position (Z-axis).

    ### Creating holes (`--hole-*` variables)

To create a hole on the surface of a `.board` or `.base` element, use the following variables, which internally use the `clip-path` property:

- `--hole-width`: Width of the hole.
- `--hole-height`: Height of the hole.
- `--hole-top`: Distance from the top edge of the parent to the top edge of the hole.
- `--hole-left`: Distance from the left edge of the parent to the left edge of the hole.

#### Example (from `sample/sam1.html`)

The following code shows how to create a hole in a `.base` element that forms part of the floor in `sample/sam1.html`:

```html
<div class="base" style="
    background-color: var(--shadow); 
    --color: white; 
    --hole-width: 130px; 
    --hole-height: 130px; 
    --hole-top: 5px; 
    --hole-left: 160px;"></div>
```

In this example, `--hole-width` and `--hole-height` set the hole size to `130px` square, and `--hole-top` and `--hole-left` position the hole at `(160px, 5px)` from the top-left of the parent. This can be used, for example, to represent a shower drain.

The `--hole-*` variables only create a hole on the surface. To add thickness (inner walls) to the hole, use the `.hollow` class together. `.hollow` should be placed at the same position and size as the hole created with `--hole-*`, and `--thick` defines the thickness of the hole.

**Example of a toilet paper holder from `sample/sam1.html`:**

```html
<div class="object left">
    <!-- Define the outer shape and hole -->
    <div class="board" style="
        --width: 20px; 
        --height: 18px; 
        --thick: 18px; 
        --hole-width: 16px; 
        --hole-height: 16px; 
        --hole-left: 2px; ..."></div>

    <!-- Create the inner wall of the hole -->
    <div class="hollow" style="
        --width: 16px; 
        --height: 16px; 
        --thick: 16px; 
        --vertical: 18px; 
        left: 2px; ..."></div>
</div>
```

Here, `.board` creates the outer holder with a `16x16px` hole, and a `.hollow` of the same size is placed to create an inner wall with `16px` thickness.

## Basic Example

This example creates a simple cube in the center of the room.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Simple Cube Example</title>
    <link rel="stylesheet" href="https://pinattutaro.github.io/room/room.css">
    <style>
        /* Option */
    </style>
</head>
<body>
    <div class="room">
        <div class="object">
            <div class="board" style="
                --width: 100px; 
                --height: 100px; 
                --thick: 100px; 
                --color: #3498db; 
                --side-color: #2980b9;"></div>
        </div>
    </div>
</body>
</html>
```

## Advanced Example

For more complex scenes demonstrating nesting, custom colors, and hole creation, see the `sample/sam1.html` file, which renders a detailed bathroom scene.