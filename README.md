# Porn
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Video Hub Dynamic</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            background-color: #121212;
            color: #fff;
            transition: background-color 0.5s ease;
        }
        header {
            background-color: #000;
            padding: 20px;
            text-align: center;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.8);
        }
        header h1 {
            margin: 0;
            color: #ff8c00;
            font-size: 2.5em;
        }
        nav {
            background-color: #333;
            padding: 10px;
            display: flex;
            justify-content: center;
        }
        nav a {
            color: #fff;
            margin: 0 15px;
            text-decoration: none;
            font-size: 1.2em;
            position: relative;
        }
        nav a::before {
            content: '';
            position: absolute;
            width: 0;
            height: 3px;
            bottom: -5px;
            left: 0;
            background-color: #ff8c00;
            visibility: hidden;
            transition: all 0.3s ease-in-out;
        }
        nav a:hover::before {
            visibility: visible;
            width: 100%;
        }
        .search-bar {
            margin: 20px;
            text-align: center;
        }
        .search-bar input[type="text"] {
            padding: 12px;
            width: 50%;
            border: none;
            border-radius: 30px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.4);
            transition: box-shadow 0.3s ease-in-out;
        }
        .search-bar input[type="text"]:focus {
            box-shadow: 0 6px 12px rgba(0, 0, 0, 0.6);
            outline: none;
        }
        .video-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 20px;
            padding: 20px;
        }
        .video-grid div {
            background-color: #1c1c1c;
            padding: 10px;
            border-radius: 10px;
            text-align: center;
            transition: transform 0.3s ease-in-out, box-shadow 0.3s ease-in-out;
            overflow: hidden;
            cursor: pointer;
        }
        .video-grid div:hover {
            transform: scale(1.05);
            box-shadow: 0 8px 20px rgba(0, 0, 0, 0.6);
        }
        .video-grid img {
            width: 100%;
            border-radius: 10px;
            transition: transform 0.3s ease-in-out;
        }
        .video-grid div:hover img {
            transform: scale(1.1);
        }
        footer {
            background-color: #000;
            padding: 10px;
            text-align: center;
            color: #777;
            position: relative;
            bottom: 0;
            width: 100%;
        }
        footer p {
            margin: 0;
        }
        /* Modal */
        .modal {
            display: none;
            position: fixed;
            z-index: 1;
            left: 0;
            top: 0;
            width: 100%;
            height: 100%;
            overflow: auto;
            background-color: rgba(0, 0, 0, 0.8);
            justify-content: center;
            align-items: center;
        }
        .modal-content {
            background-color: #333;
            padding: 20px;
            border-radius: 10px;
            max-width: 500px;
            width: 80%;
        }
        .modal-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 10px;
        }
        .modal-header h2 {
            margin: 0;
        }
        .modal-close {
            cursor: pointer;
            color: #ff8c00;
        }
        .modal-body {
            margin-bottom: 10px;
        }
        .modal-footer {
            text-align: right;
        }
        .modal-footer button {
            padding: 10px 20px;
            background-color: #ff8c00;
            color: #fff;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }
    </style>
</head>
<body>

<header>
    <h1>Video Hub</h1>
</header>

<nav>
    <a href="#">Home</a>
    <a href="#">Trending</a>
    <a href="#">Categories</a>
    <a href="#">Login</a>
</nav>

<div class="search-bar">
    <input type="text" id="searchInput" onkeyup="filterVideos()" placeholder="Search for videos...">
</div>

<div class="video-grid" id="videoGrid">
    <!-- Dynamic Video Cards will be inserted here -->
</div>

<!-- Modal for video details -->
<div class="modal" id="videoModal">
    <div class="modal-content">
        <div class="modal-header">
            <h2 id="videoTitle">Video Title</h2>
            <span class="modal-close" onclick="closeModal()">&times;</span>
        </div>
        <div class="modal-body">
            <video width="100%" controls id="videoPlayer">
                <source src="" type="video/mp4">
                Your browser does not support the video tag.
            </video>
            <p id="videoDescription">Description of the video will be here.</p>
        </div>
        <div class="modal-footer">
            <button onclick="closeModal()">Close</button>
        </div>
    </div>
</div>

<footer>
    <p>&copy; 2024 Video Hub. All rights reserved.</p>
</footer>

<script>
    // Simulating API data
    const videos = [
        { id: 1, title: 'Video Title 1', thumbnail: 'https://via.placeholder.com/200x120', description: 'Description for Video 1', videoUrl: 'https://www.w3schools.com/html/mov_bbb.mp4' },
        { id: 2, title: 'Video Title 2', thumbnail: 'https://via.placeholder.com/200x120', description: 'Description for Video 2', videoUrl: 'https://www.w3schools.com/html/movie.mp4' },
        { id: 3, title: 'Video Title 3', thumbnail: 'https://via.placeholder.com/200x120', description: 'Description for Video 3', videoUrl: 'https://www.w3schools.com/html/mov_bbb.mp4' },
        { id: 4, title: 'Video Title 4', thumbnail: 'https://via.placeholder.com/200x120', description: 'Description for Video 4', videoUrl: 'https://www.w3schools.com/html/movie.mp4' }
    ];

    // Function to dynamically load videos
    function loadVideos() {
        const videoGrid = document.getElementById('videoGrid');
        videos.forEach(video => {
            const videoCard = document.createElement('div');
            videoCard.innerHTML = `
                <img src="${video.thumbnail}" alt="${video.title}">
                <p class="video-title">${video.title}</p>
            `;
            videoCard.addEventListener('click', () => openModal(video));
            videoGrid.appendChild(videoCard);
        });
    }

    // Function to filter videos based on search input
    function filterVideos() {
        const input = document.getElementById('searchInput');
        const filter = input.value.toLowerCase();
        const videoGrid = document.getElementById('videoGrid');
        const videos = videoGrid.getElementsByTagName('div');
        for (let i = 0; i < videos.length; i++) {
            const title = videos[i].getElementsByClassName('video-title')[0];
            if (title.innerText.toLowerCase().indexOf(filter) > -1) {
                videos[i].style.display = '';
            } else {
                videos[i].style.display = 'none';
            }
        }
