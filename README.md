<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Random Book Selector</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f4;
            margin: 0;
            padding: 0;
        }
        #container {
            max-width: 600px;
            margin: 20px auto;
            background-color: #fff;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }
        h1 {
            text-align: center;
            margin-bottom: 20px;
        }
        label {
            font-weight: bold;
        }
        select, button {
            display: block;
            width: 100%;
            padding: 10px;
            margin-bottom: 10px;
            border: 1px solid #ccc;
            border-radius: 4px;
            box-sizing: border-box;
        }
        button {
            background-color: #007bff;
            color: #fff;
            border: none;
            cursor: pointer;
        }
        button:hover {
            background-color: #0056b3;
        }
    </style>
</head>
<body>
    <div id="container">
        <h1>Random Book Selector</h1>
        <label for="category">Select a category:</label>
        <select id="category">
            <option value="fiction">Fiction</option>
            <option value="non-fiction">Non-Fiction</option>
        </select>
        <button onclick="selectRandomBook()">Select Random Book</button>
        <div id="random-book"></div>
    </div>

    <script>
        async function fetchBooks(category) {
            try {
                const response = await fetch(`https://api.example.com/books?category=${category}`);
                if (!response.ok) {
                    throw new Error('Failed to fetch book data');
                }
                const data = await response.json();
                return data.books;
            } catch (error) {
                console.error(error);
                return [];
            }
        }

        async function selectRandomBook() {
            const category = document.getElementById("category").value;
            const books = await fetchBooks(category);
            if (books.length > 0) {
                const randomIndex = Math.floor(Math.random() * books.length);
                const randomBook = books[randomIndex];
                document.getElementById("random-book").innerText = `Randomly Selected Book: ${randomBook.title}`;
            } else {
                document.getElementById("random-book").innerText = 'No books found in the selected category';
            }
        }
    </script>
</body>
</html>



import requests
import random

def fetch_books(category):
    # Make a request to the Goodreads API to fetch books in the specified category
    url = f"https://www.goodreads.com/shelf/book/{category}.json?key=YOUR_API_KEY"
    try:
        response = requests.get(url)
        response.raise_for_status()  # Raise an error for bad response status codes
        data = response.json()
        return [book["title"] for book in data["books"]]
    except requests.exceptions.RequestException as e:
        print(f"Failed to fetch book data from Goodreads: {e}")
        return []

def select_random_book(books):
    # Select a random book from the list of books
    return random.choice(books)

def main():
    print("Welcome to the Random Book Selector!")
    category = input("Choose a category (e.g., fiction, non-fiction): ")
    books = fetch_books(category)
    if books:
        random_book = select_random_book(books)
        print(f"Randomly selected book from the '{category}' category: {random_book}")
    else:
        print("No books found in the specified category.")

if __name__ == "__main__":
    main()

