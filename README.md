<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>My GitHub Portfolio</title>
    <link href="https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Roboto', sans-serif;
            margin: 0;
            padding: 0;
            background-color: #0a0a0a; /* Jet black background */
            color: #ecf0f1;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            flex-direction: column;
            text-align: center;
        }

        h1 {
            color: #ecf0f1;
            margin-top: 20px;
            font-size: 2.5em;
        }

        .username {
            font-size: 1.5em;
            color: #3498db;
            margin-top: 20px;
        }

        /* Navbar Style */
        .navbar {
            position: fixed;
            top: 0;
            width: 100%;
            background-color: #001f3d; /* Navy blue background */
            padding: 10px 0;
            text-align: center;
            z-index: 1000;
        }

        .navbar a {
            color: #ecf0f1;
            padding: 14px 20px;
            text-decoration: none;
            font-size: 18px;
            text-transform: uppercase;
            transition: background-color 0.3s;
        }

        .navbar a:hover {
            background-color: #3498db;
        }

        .container {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
            gap: 20px;
            width: 80%;
            max-width: 1200px;
            margin-top: 50px; /* Adjust for the navbar */
            justify-items: center;
            align-items: center;
            margin-left: auto;
            margin-right: auto;
        }

        .card {
            background: #34495e;
            border-radius: 8px;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.3);
            padding: 20px;
            text-align: center;
            transition: transform 0.3s ease-in-out, box-shadow 0.3s ease-in-out;
            cursor: pointer;
            width: 300px; /* Set a consistent width for all cards */
            height: 200px; /* Set a consistent height for all cards */
            margin: 10px; /* Add margin around each card */
        }

        .card:hover {
            transform: translateY(-8px);
            box-shadow: 0 15px 30px rgba(0, 0, 0, 0.6);
        }

        .card h3 {
            color: #ecf0f1;
            margin-bottom: 15px;
        }

        .card p {
            color: #bdc3c7;
            margin-bottom: 20px;
        }

        /* Button Style */
        .view-button, .insights-button {
            display: inline-block;
            background-color: #3498db;
            color: white;
            padding: 12px 25px;
            border-radius: 4px;
            text-decoration: none;
            transition: background-color 0.3s;
            margin-top: 10px;
        }

        .view-button:hover, .insights-button:hover {
            background-color: #2980b9;
        }

        .insights-button {
            background-color: #1abc9c;
        }

        .insights-button:hover {
            background-color: #16a085;
        }

        .footer {
            margin-top: 30px;
            text-align: center;
            font-size: 14px;
            color: #bdc3c7;
        }

        .footer a {
            color: #3498db;
            text-decoration: none;
        }

        /* Add margin and grid gap to repository container */
        #repoContainer {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(280px, 1fr)); /* Adjust to your layout */
            gap: 80px; /* Add gap between the cards */
            margin-top: 50px;
            margin-left: auto;
            margin-right: auto;
            justify-items: center;
            align-items: start;
        }

        @media screen and (max-width: 768px) {
            .container {
                width: 95%;
            }
        }
    </style>
</head>
<body>

    <!-- Navbar -->
    <div class="navbar">
        <a href="#" id="homeLink">Home</a>
        <a href="#" id="codesLink">Codes</a>
        <a href="#" id="assignmentsLink">Assignments</a>
        <a href="#" id="projectsLink">Projects</a>
        <a href="https://github.com/VARUNs2196">GitHub Profile</a> <!-- Added GitHub Profile link -->
    </div>

    <!-- Username Section -->
    <div class="username" id="usernameDisplay" style="margin-top: -50px;">Loading...</div>
    
    <h1>My GitHub Portfolio</h1>

    <!-- Category Cards -->
    <div class="container" id="categoryContainer" style="margin-left: 350px;">
        <div class="card" id="codesCard" style="margin-right: 150px;">
            <h3>Codes</h3>
            <p>Explore my coding repositories</p>
        </div>
        <div class="card" id="assignmentsCard" style="margin-right: 50px;margin-left: 50px;">
            <h3>Assignments</h3>
            <p>Explore my assignments repositories</p>
        </div>
        <div class="card" id="projectsCard" style="margin-left: 150px;">
            <h3>Projects</h3>
            <p>Explore my project repositories</p>
        </div>
    </div>

    <!-- Repository Cards will be dynamically added here -->
    <div class="container" id="repoContainer" style="display: none;"></div>

    <div class="footer" style="margin-bottom:-120px ; margin-top: 120px;">
        <p>Check out my <a href="https://github.com/VARUNs2196">GitHub Profile</a></p>
    </div>

    <script>
        const username = 'Govindg1211'; // Replace with your GitHub username
        const categoryContainer = document.getElementById('categoryContainer');
        const repoContainer = document.getElementById('repoContainer');
        const usernameDisplay = document.getElementById('usernameDisplay');
        const categoryLinks = {
            codes: document.getElementById('codesLink'),
            assignments: document.getElementById('assignmentsLink'),
            projects: document.getElementById('projectsLink'),
            home: document.getElementById('homeLink')
        };
        
        const codesCard = document.getElementById('codesCard');
        const assignmentsCard = document.getElementById('assignmentsCard');
        const projectsCard = document.getElementById('projectsCard');
        
        // Fetch user data from GitHub API
        fetch(`https://api.github.com/users/${username}`)
            .then(response => response.json())
            .then(data => {
                usernameDisplay.textContent = `Welcome, ${data.login}!`;
            })
            .catch(error => {
                console.error('Error fetching username:', error);
                usernameDisplay.textContent = 'Error fetching username';
            });
        
        // Hide repository container initially
        repoContainer.style.display = 'none';
        
        // Define repositories and Insights links for each category
        const categoryRepos = {
            'codes': [
                { name: 'repo1', insightsLink: 'https://example.com/insights/codes/repo1' },
                { name: 'repo2', insightsLink: 'https://example.com/insights/codes/repo2' },
                { name: 'repo3', insightsLink: 'https://example.com/insights/codes/repo3' }
            ],
            'assignments': [
                { name: 'Assignments'},
                { name: 'assignment2'}
            ],
            'projects': [
                { name: 'Stock-Price-Tracker', insightsLink: 'https://govindg1211.github.io/stock-price-tracker/' },
                { name: 'URL-DOWNLOADER', insightsLink: 'https://govindg1211.github.io/URL-downloader/' },
                { name: 'File-Organiser', insightsLink: 'https://govindg1211.github.io/file-organiser/' },
                { name: 'Budget-tracker', insightsLink: 'https://govindg1211.github.io/budget-tracker/' }
            ]
        };
        
        // Fetch repositories based on category
        function fetchRepos(category) {
            const repos = categoryRepos[category];
            if (repos && repos.length > 0) {
                showRepos(repos);
            } else {
                alert('No repositories available for this category.');
            }
        }
        
        // Function to display the repositories
        function showRepos(repos) {
            // Clear previous repositories
            repoContainer.innerHTML = '';
        
            // Add each repository as a card
            repos.forEach(repo => {
                fetch(`https://api.github.com/repos/${username}/${repo.name}`)
                    .then(response => response.json())
                    .then(repoData => {
                        const card = document.createElement('div');
                        card.classList.add('card');
        
                        card.innerHTML = `
                            <h3>${repoData.name}</h3>
                            <p>${repoData.description ? repoData.description : 'No description available'}</p>
                            <a class="view-button" href="${repoData.html_url}">View Repository</a>
                            <br>
                            <a class="insights-button" href="${repo.insightsLink}">Insights</a>
                        `;
        
                        repoContainer.appendChild(card);
                    })
                    .catch(error => {
                        console.error('Error fetching repository:', error);
                    });
            });
        
            // Show the repository container and hide the category container
            categoryContainer.style.display = 'none';
            repoContainer.style.display = 'grid';
        }
        
        // Set up category click event listeners for cards
        codesCard.addEventListener('click', () => fetchRepos('codes'));
        assignmentsCard.addEventListener('click', () => fetchRepos('assignments'));
        projectsCard.addEventListener('click', () => fetchRepos('projects'));
        
        // Set up category click event listeners for navbar
        categoryLinks.codes.addEventListener('click', (event) => {
            event.preventDefault();
            fetchRepos('codes');
        });
        
        categoryLinks.assignments.addEventListener('click', (event) => {
            event.preventDefault();
            fetchRepos('assignments');
        });
        
        categoryLinks.projects.addEventListener('click', (event) => {
            event.preventDefault();
            fetchRepos('projects');
        });
        
        // Set up home link click to go back to categories
        categoryLinks.home.addEventListener('click', (event) => {
            event.preventDefault();
            repoContainer.style.display = 'none';
            categoryContainer.style.display = 'grid';
        });
    </script>
    
    
    

</body>
</html>
