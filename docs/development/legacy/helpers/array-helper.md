---
lang: php
---

<!--
    This source file is part of the open source project
    ExpressionEngine User Guide (https://github.com/ExpressionEngine/ExpressionEngine-User-Guide)

    @link      https://expressionengine.com/
    @copyright Copyright (c) 2003-2019, EllisLab Corp. (https://ellislab.com)
    @license   https://expressionengine.com/license Licensed under Apache License, Version 2.0
-->

# Array Helper

The Array Helper file contains functions that assist in working with arrays. This helper is loaded using the following code:

    ee()->load->helper('array');

## Available Functions

[TOC=3]

### `element($item, $array[, $default = NULL])`

| Parameter | Type     | Description                             |
| --------- | -------- | --------------------------------------- |
| \$item    | `String` | Item to fetch from the array            |
| \$array   | `Array`  | Input array                             |
| \$default | `Bool`   | What to return if the array isn't valid |
| Returns   | `Mixed`  | NULL on failure or the array item.      |

Lets you fetch an item from an array. The function tests whether the array index is set and whether it has a value. If a value exists it is returned. If a value does not exist it returns NULL, or whatever you've specified as the default value via the third parameter.

    $array = array(
        'color' => 'red',
        'shape' => 'round',
        'size'  => ''
    );

    echo element('color', $array); // returns "red"
    echo element('size', $array, 'foobar'); // returns "foobar"

### `elements($items, $array[, $default = NULL])`

| Parameter | Type     | Description                             |
| --------- | -------- | --------------------------------------- |
| \$item    | `String` | Item to fetch from the array            |
| \$array   | `Array`  | Input array                             |
| \$default | `Bool`   | What to return if the array isn't valid |
| Returns   | `Mixed`  | NULL on failure or the array item.      |

Lets you fetch a number of items from an array. The function tests whether each of the array indices is set. If an index does not exist it is set to NULL, or whatever you've specified as the default value via the third parameter.

    $array = array(
        'color' => 'red',
        'shape' => 'round',
        'radius' => '10',
        'diameter' => '20'
    );

    $my_shape = elements(array('color', 'shape', 'height'), $array);

The above will return the following array:

    array(
        'color' => 'red',
        'shape' => 'round',
        'height' => NULL
    );

You can set the third parameter to any default value you like.

    $my_shape = elements(array('color', 'shape', 'height'), $array, 'foobar');

The above will return the following array:

    array(     
        'color'     => 'red',
        'shape'     => 'round',
        'height'    => 'foobar'
    );

This is useful when sending the `$_POST` array to one of your Models. This prevents users from sending additional POST data to be entered into your tables.

    ee()->load->model('post_model');
    ee()->post_model->update(
        elements(array('id', 'title', 'content'), $_POST)
    );

This ensures that only the id, title and content fields are sent to be updated.

### `random_element($array)`

| Parameter | Type    | Description                     |
| --------- | ------- | ------------------------------- |
| \$array   | `Array` | Input array                     |
| Returns   | `Mixed` | A random element from the array |

Takes an array as input and returns a random element from it.

Usage example:

    $quotes = array(
        "I find that the harder I work, the more luck I seem to have. - Thomas Jefferson",
        "Don't stay in bed, unless you can make money in bed. - George Burns",
        "We didn't lose the game; we just ran out of time. - Vince Lombardi",
        "If everything seems under control, you're not going fast enough. - Mario Andretti",
        "Reality is merely an illusion, albeit a very persistent one. - Albert Einstein",
        "Chance favors the prepared mind - Louis Pasteur"
    );

    echo random_element($quotes);