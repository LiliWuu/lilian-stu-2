---
toc: true
comments: true
layout: post
title: Data Table for Snake Game
description: This is where I will keep my the contents of my data table for the snake game.
type: tangibles
courses: { compsci: {week: 3} }
---

### Data Table 
---

<h2>HTML Cell Output from Jupyter</h2>

<!-- Head contains information to Support the Document -->
<head>
    <!-- load jQuery and DataTables output style and scripts -->
    <link rel="stylesheet" type="text/css" href="https://cdn.datatables.net/1.13.4/css/jquery.dataTables.min.css">
    <script type="text/javascript" language="javascript" src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
    <script>var define = null;</script>
    <script type="text/javascript" language="javascript" src="https://cdn.datatables.net/1.13.4/js/jquery.dataTables.min.js"></script>
</head>

<!-- Body contains the contents of the Document -->
<body>
    <table id="snake_game" class="table">
        <thead>
            <tr>
                <th>Name</th>
                <th>Speed</th>
                <th>Trials</th>
                <th>High Score</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td>Lilian</td>
                <td>Fast</td>
                <td>1</td>
                <td>6</td>
            </tr>
            <tr>
                <td>Lilian</td>
                <td>Fast</td>
                <td>2</td>
                <td>7</td>
            </tr>
            <tr>
                <td>Lilian</td>
                <td>Fast</td>
                <td>3</td>
                <td>6</td>
            </tr>
            </hr>
            <tr>
                <td>Vrnda</td>
                <td>Fast</td>
                <td>1</td>
                <td>1</td>
            </tr>
            <tr>
                <td>Vrnda</td>
                <td>Fast</td>
                <td>2</td>
                <td>2</td>
            </tr>
            <tr>
                <td>Vrnda</td>
                <td>Fast</td>
                <td>3</td>
                <td>3</td>
            </tr>
            <tr>
                <td>Kayla</td>
                <td>Fast</td>
                <td>1</td>
                <td>8</td>
            </tr>
            <tr>
                <td>Kayla</td>
                <td>Fast</td>
                <td>2</td>
                <td>3</td>
            </tr>
            <tr>
                <td>Kayla</td>
                <td>Fast</td>
                <td>3</td>
                <td>2</td>
            </tr>
        </tbody>
    </table>
</body>

<!-- Script is used to embed executable code -->
<script>
    $("#snake_game").DataTable();
</script>

---
## Suggestions on How to Effectively Use the Table
In the search bar...
- Type in certain trial numbers to filter out the other trial numbers
    - Allows for easier comparison of the data


