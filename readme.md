jquery.Table
============

JQuery plugin for table data management, input and manipulation. Supports inline editing, formula based calculations, data typing, value formatting and keyboard navigation. 

Example:
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="utf-8" />
    <script type="text/javascript" src="jquery/jquery-1.11.2.min.js"></script>

    <link rel="stylesheet" type="text/css" href="jquery.Table/css/table.css" />
    <script type="text/javascript" src="jquery.Table/js/table.js"></script>

    <script type="text/javascript">

        // Instantiate the table object and define its 
        var t = new Table({
            // id of table to attach to
            id: "example",
            // Table header fields, data types and classes
            fields: {
                "Date": {
                    "class": "edit",
                    "type": "date"
                }, 
                "Meter Read": {
                    "class": "edit",
                    "type": "int"
                },
                "Used kWh": {
                    "type": "calc",
                    "formula": [
                        { "subtract": [{ "c":-1 }, { "c":-1, "r":-1 }] }
                    ]
                },
                "Cost": {
                    "class": "edit",
                    "type": "money"
                }, 
                "Avg kWh / Day": {
                    "type": "calc",
                    "formula": [
                        { "datediff": [{ "c":-4 }, { "c":-4, "r":-1 }] },
                        { "divide": [{ "c":-2 }, { }] }
                    ]
                },
                "Avg Cost / Day": {
                    "class": "money",
                    "type": "calc",
                    "formula": [
                        { "datediff": [{ "c":-5 }, { "c":-5, "r":-1 }] },
                        { "divide": [{ "c":-2 }, { }] }
                    ]
                }
            },
            // Table data
            data: [
                ['2014-12-04', '45653', '', '205.26', '', ''],
                ['2015-02-04', '47017', '', '236.81', '', '']
                
            ],
            // Enable debug output to console
            debug: true
        });

        $(document).ready(function() {

            // Render the table
            t.render();

            // Add row
            $("button#addrow").on("click", function() {
                t.addRow({ "position": "top" });
            });

            // Serialize
            $("button#serialize").on("click", function() {
                var data = t.serialize();
                console.log(data);
            });
        }

    </script>
</head>
<body>

    <button id="addrow">Add Row</button>
    <button id="serialize">Serialize</button>
    <table id="example"></table>

</body>
</html>
```