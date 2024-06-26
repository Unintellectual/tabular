# tabular - Easily pretty-print tabular data

## Summary

Tabular - Generic Go Library for easy pretty-printing of tabular data.

## Installation

    go get github.com/Unintellectual/tabular

## Description

Supported data types:

- 2D Array of `Int`, `Int64`, `Float64`, `String`, `interface{}`
- Map of `String`, `interface{}` (Keys will be used as header)

## Usage

```go
// Create Some Fake Rows
row_1 := []interface{}{"Mark", 15, "ready"}
row_2 := []interface{}{"Unintellectual", 20, "ready"}

// Create an object from 2D interface array
t := gotabular.Create([][]interface{}{row_1, row_2})

// Set the Headers (optional)
t.SetHeaders([]string{"age", "status"})

// Set the Empty String (optional)
t.SetEmptyString("None")

// Set Align (Optional)
t.SetAlign("right")

// Print the result: grid, or simple
fmt.Println(t.Render("grid"))

+---------+--------+-----------+
|         |    age |    status |
+=========+========+===========+
|    john |     20 |     ready |
+---------+--------+-----------+
|    bndr |     23 |     ready |
+---------+--------+-----------+
```

## Example with String

```go
// Some Strings
string_1 := []string{"TV", "1000$", "Sold"}
string_2 := []string{"PC", "50%", "on Hold"}

// Create Object
tabular := gotabular.Create([][]string{string_1, string_2})

// Set Headers
tabular.SetHeaders([]string{"Type", "Cost", "Status"})

// Render
fmt.Println(tabular.Render("simple"))

---------  ----------  ------------
    Type        Cost        Status
---------  ----------  ------------
      TV       1000$          Sold

      PC         50%       on Hold
---------  ----------  ------------
```

## Example with String Wrapping

```go
tabular := gotabular.Create([][]string{[]string{"Lorem ipsum dolor sit amet, consectetur adipiscing elit. Vivamus laoreet vestibulum pretium. Nulla et ornare elit. Cum sociis natoque penatibus et magnis",
	"Vivamus laoreet vestibulum pretium. Nulla et ornare elit. Cum sociis natoque penatibus et magnis", "zzLorem ipsum", " test", "test"}, []string{"Lorem ipsum dolor sit amet, consectetur adipiscing elit. Vivamus laoreet vestibulum pretium. Nulla et ornare elit. Cum sociis natoque penatibus et magnis",
	"Vivamus laoreet vestibulum pretium. Nulla et ornare elit. Cum sociis natoque penatibus et magnis", "zzLorem ipsum", " test", "test"}, STRING_ARRAY, []string{"Lorem ipsum dolor sit amet, consectetur adipiscing elit. Vivamus laoreet vestibulum pretium. Nulla et ornare elit. Cum sociis natoque penatibus et magnis",
	"Vivamus laoreet vestibulum pretium. Nulla et ornare elit. Cum sociis natoque penatibus et magnis", "zzLorem ipsum", " test", "test"}, STRING_ARRAY})

tabular.SetHeaders([]string{"Header 1", "header 2", "header 3", "header 4"})
// Set Max Cell Size
tabular.SetMaxCellSize(16)

// Turn On String Wrapping
tabular.SetWrapStrings(true)

// Render the table
fmt.Println(tabular.Render("grid"))

+---------------------+---------------------+----------------+-------------+-------------+
|                     |            Header 1 |       header 2 |    header 3 |    header 4 |
+=====================+=====================+================+=============+=============+
|    Lorem ipsum dolo |    Vivamus laoreet  |    Lorem ipsum |        test |        test |
|    r sit amet, cons |    vestibulum preti |                |             |             |
|    ectetur adipisci |    um. Nulla et orn |                |             |             |
|    ng elit. Vivamus |    are elit. Cum so |                |             |             |
|     laoreet vestibu |    ciis natoque pen |                |             |             |
|    lum pretium. Nul |    atibus et magnis |                |             |             |
|    la et ornare eli |                     |                |             |             |
|    t. Cum sociis na |                     |                |             |             |
|    toque penatibus  |                     |                |             |             |
|           et magnis |                     |                |             |             |
+---------------------+---------------------+----------------+-------------+-------------+
|    Lorem ipsum dolo |    Vivamus laoreet  |    Lorem ipsum |        test |        test |
|    r sit amet, cons |    vestibulum preti |                |             |             |
|    ectetur adipisci |    um. Nulla et orn |                |             |             |
|    ng elit. Vivamus |    are elit. Cum so |                |             |             |
|     laoreet vestibu |    ciis natoque pen |                |             |             |
|    lum pretium. Nul |    atibus et magnis |                |             |             |
|    la et ornare eli |                     |                |             |             |
|    t. Cum sociis na |                     |                |             |             |
|    toque penatibus  |                     |                |             |             |
|           et magnis |                     |                |             |             |
+---------------------+---------------------+----------------+-------------+-------------+
|         test string |       test string 2 |           test |         row |        bndr |
+---------------------+---------------------+----------------+-------------+-------------+
|    Lorem ipsum dolo |    Vivamus laoreet  |    Lorem ipsum |        test |        test |
|    r sit amet, cons |    vestibulum preti |                |             |             |
|    ectetur adipisci |    um. Nulla et orn |                |             |             |
|    ng elit. Vivamus |    are elit. Cum so |                |             |             |
|     laoreet vestibu |    ciis natoque pen |                |             |             |
|    lum pretium. Nul |    atibus et magnis |                |             |             |
|    la et ornare eli |                     |                |             |             |
|    t. Cum sociis na |                     |                |             |             |
|    toque penatibus  |                     |                |             |             |
|           et magnis |                     |                |             |             |
+---------------------+---------------------+----------------+-------------+-------------+
|         test string |       test string 2 |           test |         row |        bndr |
+---------------------+---------------------+----------------+-------------+-------------+
```

## Examples

```go
t := gotabular.Create([][]string{STRING_ARRAY, STRING_ARRAY})

t.SetHeaders(HEADERS) // If not headers are set, the first row will be used.

t.SetEmptyString("None") // Set what will be printed in the empty cell

rendered_string := t.Render("simple") // Render() will return a string

Simple Table
----------------------  ----------------------  ----------------------  -------------  -------------
             Header 1                Header 2                Header 3       Header 4       Header 5
----------------------  ----------------------  ----------------------  -------------  -------------
          test string           test string 2                    test            row           bndr

          test string           test string 2                    test            row           bndr

    4th element empty       4th element empty       4th element empty           None           None
----------------------  ----------------------  ----------------------  -------------  -------------

Grid Table (Align Right)
+-------------+-------------+-------------+-------------+-------------+
|    Header 1 |    Header 2 |    Header 3 |    Header 4 |    Header 5 |
+=============+=============+=============+=============+=============+
|       10.01 |      12.002 |      -123.5 |    20.00005 |        1.01 |
+-------------+-------------+-------------+-------------+-------------+
|       10.01 |      12.002 |      -123.5 |    20.00005 |        1.01 |
+-------------+-------------+-------------+-------------+-------------+
|       10.01 |      12.002 |      -123.5 |    20.00005 |        None |
+-------------+-------------+-------------+-------------+-------------+

Padded Headers:
+----------------------+----------------------+----------------------+-------------+-------------+
|                      |             Header 1 |             header 2 |    header 3 |    header 4 |
+======================+======================+======================+=============+=============+
|          test string |        test string 2 |                 test |         row |        bndr |
+----------------------+----------------------+----------------------+-------------+-------------+
|          test string |        test string 2 |                 test |         row |        bndr |
+----------------------+----------------------+----------------------+-------------+-------------+
|    4th element empty |    4th element empty |    4th element empty |        None |        None |
+----------------------+----------------------+----------------------+-------------+-------------+

Align Center:
+-------------+-------------+-------------+-------------+-------------+
|   Header 1  |   Header 2  |   Header 3  |   Header 4  |   Header 5  |
+=============+=============+=============+=============+=============+
|    10.01    |    12.002   |    -123.5   |   20.00005  |     1.01    |
+-------------+-------------+-------------+-------------+-------------+
|    10.01    |    12.002   |    -123.5   |   20.00005  |     1.01    |
+-------------+-------------+-------------+-------------+-------------+
|    10.01    |    12.002   |    -123.5   |   20.00005  |     1.01    |
+-------------+-------------+-------------+-------------+-------------+

Align Left:
+-------------+-------------+-------------+-------------+-------------+
| Header 1    | Header 2    | Header 3    | Header 4    | Header 5    |
+=============+=============+=============+=============+=============+
| 10.01       | 12.002      | -123.5      | 20.00005    | 1.01        |
+-------------+-------------+-------------+-------------+-------------+
| 10.01       | 12.002      | -123.5      | 20.00005    | 1.01        |
+-------------+-------------+-------------+-------------+-------------+
| 10.01       | 12.002      | -123.5      | 20.00005    | 1.01        |
+-------------+-------------+-------------+-------------+-------------+
```

## Contribute

All Contributions are welcome. The todo list is on the bottom of this README. Feel free to send a pull request.

## License

GNU GENERAL PUBLIC LICENSE

## TODO

- [ ] Add more examples
- [ ] Better Documentation
- [ ] Implement more data table formats
- [ ] Decimal point alignment for floats

## Acknowledgement

Inspired by Python package [tabulate](https://pypi.python.org/pypi/tabulate)
