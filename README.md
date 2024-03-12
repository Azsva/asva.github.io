# asva.github.io
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Random Book Selector</title>
    <style>
        /* Add your CSS styles here */
    </style>
</head>
<body>
    <h1>Random Book Selector</h1>
    
    <!-- Category Selection -->
    <label for="category">Select a category:</label>
    <select id="category">
        <option value="fiction">Fiction</option>
        <option value="non-fiction">Non-Fiction</option>
        <!-- Add more categories as needed -->
    </select>
    <br><br>
    
    <!-- Button to Select Random Book -->
    <button onclick="selectRandomBook()">Select Random Book</button>
    
    <!-- Display Area for Randomly Selected Book -->
    <div id="random-book"></div>
    
    <script>
        function selectRandomBook() {
            var category = document.getElementById("category").value;
            var books;
            
            // Book Database (Add more books as needed)
            if (category === "fiction") {
                books = ["Book 1", "Book 2", "Book 3", "Book 4"];
            } else if (category === "non-fiction") {
                books = ["Book A", "Book B", "Book C", "Book D"];
            }
            
            // Randomly select a book
            var randomIndex = Math.floor(Math.random() * books.length);
            var randomBook = books[randomIndex];
            
            // Display the selected book
            document.getElementById("random-book").innerText = "Randomly Selected Book: " + randomBook;
        }
    </script>
</body>
</html>
