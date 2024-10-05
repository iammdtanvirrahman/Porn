<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>My Articles</title>
    <link rel="stylesheet" href="css/styles.css">
</head>
<body>
    <header>
        <div class="container">
            <h1>Welcome to My Articles</h1>
            <nav>
                <ul>
                    <li><a href="index.html">Home</a></li>
                    <li><a href="articles/article1.html">First Article</a></li>
                    <li><a href="articles/article2.html">Second Article</a></li>
                    <li><a href="articles/article3.html">Third Article</a></li>
                </ul>
            </nav>
        </div>
    </header>

    <main class="container">
        <section>
            <h2>Latest Articles</h2>
            <div class="articles">
                <article>
                    <h3><a href="articles/article1.html">Article 1 Title</a></h3>
                    <p>Summary of the first article. This is a short description that gives an overview of the article content.</p>
                </article>

                <article>
                    <h3><a href="articles/article2.html">Article 2 Title</a></h3>
                    <p>Summary of the second article. This is a short description that gives an overview of the article content.</p>
                </article>

                <article>
                    <h3><a href="articles/article3.html">Article 3 Title</a></h3>
                    <p>Summary of the third article. This is a short description that gives an overview of the article content.</p>
                </article>
            </div>
        </section>
    </main>

    <footer>
        <p>&copy; 2024 My Articles. All rights reserved.</p>
    </footer>
</body>
</html>
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Article 3</title>
    <link rel="stylesheet" href="../css/styles.css">
</head>
<body>
    <header>
        <div class="container">
            <h1>Article 3 Title</h1>
            <nav>
                <ul>
                    <li><a href="../index.html">Home</a></li>
                </ul>
            </nav>
        </div>
    </header>

    <main class="container">
        <section>
            <h2>Article 3</h2>
            <p>Here’s the full content of your third article. You can write whatever you want here!</p>
        </section>
    </main>

    <footer>
        <p>&copy; 2024 My Articles. All rights reserved.</p>
    </footer>
</body>

</html>
body {
    font-family: Arial, sans-serif;
    margin: 0;
    padding: 0;
    background-color: #f4f4f4;
}

.container {
    width: 80%;
    margin: auto;
    overflow: hidden;
}

header {
    background: linear-gradient(to right, #6a11cb, #2575fc);
    color: white;
    padding: 20px 0;
    text-align: center;
}

header h1 {
    margin: 0;
    font-size: 2.5em;
}

nav ul {
    list-style-type: none;
    padding: 0;
}

nav ul li {
    display: inline;
    margin: 0 15px;
}

nav ul li a {
    color: white;
    text-decoration: none;
    font-weight: bold;
}

nav ul li a:hover {
    text-decoration: underline;
}

main {
    padding: 20px;
}

section {
    background-color: white;
    padding: 20px;
    border-radius: 5px;
    box-shadow: 0 2px 5px rgba(0,0,0,0.1);
    margin-bottom: 20px;
}

h2 {
    color: #333;
}

.articles {
    display: flex;
    flex-direction: column;
    gap: 20px;
}

article {
    background-color: #e9ecef;
    border-radius: 5px;
    padding: 15px;
    transition: background-color 0.3s;
}

article:hover {
    background-color: #d1d1d1;
}

article h3 {
    margin: 0;
    color: #333;
}

article p {
    color: #666;
}

footer {
    text-align: center;
    padding: 15px;
    background-color: #333;
    color: white;
}
git add .
git commit -m "Enhanced website design and added third article"
git push origin main