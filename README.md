 # GitHub Synced Portfolio

A personal portfolio that automatically pulls my projects from GitHub.

I wanted to build a portfolio where I don't have to manually add a new project every time I create something.

Normally, adding a project means editing a JSON file, adding an image, writing the project details, and deploying the website again.

I wanted to avoid all of that.

The idea is simple:

```text
Build a project
      ↓
Push it to GitHub
      ↓
Portfolio detects the repository
      ↓
Project appears automatically
```

So my GitHub repositories act as the main source for my projects.

---

## How it works

The portfolio uses the GitHub API to fetch my public repositories.

For example:

```text
GitHub
└── BipinDev404
    ├── BeepCinema
    ├── Quizzy
    ├── Baula
    ├── Momate
    └── YuvaUpdate
```

The website fetches these repositories and converts them into project cards.

Each project can show information such as:

* Project name
* Description
* GitHub link
* Live demo
* Programming language
* Topics
* Stars
* Forks
* Last updated date

Most of this information already exists in GitHub, so there is no reason to maintain it separately.

---

## The main idea

The most important part of this project is that I don't want to maintain two separate lists.

I don't want this:

```text
GitHub Projects
       +
Portfolio Projects
```

because eventually they will become different.

Instead:

```text
              GitHub
                 │
                 │
                 ▼
            GitHub API
                 │
                 ▼
             Portfolio
```

GitHub is the source of truth.

---

## Adding a new project

Adding a project should be as simple as creating a repository.

For example, I create:

```text
my-new-project
```

Then I add a repository description:

```text
A small web application for managing daily tasks.
```

I can also add GitHub topics:

```text
javascript
web-app
productivity
```

And if the project has a live website, I add the URL as the repository homepage.

After pushing the project to GitHub, the portfolio can pick it up automatically.

There is no need to edit the portfolio source code.

---

## Project data

GitHub already provides most of the information required by the portfolio.

For example, a repository contains data similar to:

```json
{
  "name": "BeepCinema",
  "description": "A modern movie discovery website",
  "html_url": "https://github.com/...",
  "homepage": "https://...",
  "language": "JavaScript",
  "topics": [
    "movie",
    "javascript",
    "web-development"
  ],
  "stargazers_count": 10,
  "forks_count": 2
}
```

The portfolio simply uses this information to create the project UI.

---

## Live Demo

I also wanted the portfolio to understand whether a project has a live website.

GitHub repositories have a `homepage` field, so I can use that for the live demo.

For example:

```text
Repository
    ↓
homepage
    ↓
https://my-project.vercel.app
```

Then the project card can show:

```text
[ Live Demo ]  [ GitHub ]
```

If there is no homepage, only the GitHub button is shown.

---

## Featured projects

Not every repository needs to be highlighted on the homepage.

For that, I can keep a small configuration file containing only portfolio-specific information.

For example:

```json
{
  "featured": [
    "BeepCinema",
    "Momate",
    "Quizzy"
  ]
}
```

The actual project information still comes from GitHub.

This means I'm only manually controlling things that GitHub doesn't know about.

---

## Project overrides

Sometimes I may want to customize something.

For example:

```json
{
  "BeepCinema": {
    "featured": true,
    "image": "/projects/beepcinema.png",
    "customDescription": "A modern movie discovery platform."
  }
}
```

This allows me to add custom portfolio information without copying the entire repository data.

---

## Searching and filtering

Since all projects come from GitHub, the portfolio can also provide useful filters.

For example:

```text
All
Web
Android
Games
AI
Cybersecurity
```

The categories can be based on GitHub repository topics.

There can also be a simple project search:

```text
Search projects...
```

which searches through project names, descriptions, topics, and languages.

---

## Project details

Clicking a project opens a dedicated project page.

Something like:

```text
BeepCinema

A modern movie discovery website.

JavaScript · HTML · CSS · Firebase

[ Live Demo ] [ GitHub ]

Stars: 10
Forks: 2

README
-------------------------
Project documentation...
```

The repository README can also be fetched and displayed on the project page.

This means the GitHub repository remains the place where I document the project.

---

## Architecture

The basic architecture is pretty simple:

```text
GitHub
   │
   ▼
GitHub API
   │
   ▼
Portfolio
   │
   ├── Project Cards
   ├── Search
   ├── Filters
   └── Project Details
```

For a simple version, the frontend can directly request public GitHub repositories.

For a more production-ready version, GitHub data can be fetched through a backend/API route and cached.

---

## Caching

GitHub API requests don't need to happen every time a component renders.

A cache can be added so that the portfolio doesn't repeatedly request the same data.

For example:

```text
Portfolio
    ↓
Cache
    ↓
GitHub API
```

This also helps with GitHub API rate limits.

---

## Design

The portfolio is mainly focused on the projects rather than having a huge traditional portfolio layout.

The design should stay:

* Minimal
* Modern
* Fast
* Responsive
* Developer-focused

The projects are the main part of the website.

---

## Possible stack

The project can be built with something like:

```text
Next.js
React
TypeScript
Tailwind CSS
GitHub REST API
```

But the concept doesn't depend on a particular framework.

The important part is the GitHub synchronization.

---

## Folder structure

A possible structure:

```text
portfolio/
│
├── app/
│
├── components/
│   ├── Navbar
│   ├── ProjectCard
│   ├── ProjectGrid
│   └── ProjectDetails
│
├── lib/
│   └── github
│
├── data/
│   └── project-overrides.json
│
├── public/
│   └── projects/
│
└── README.md
```

---

## The workflow I want

Eventually, maintaining the portfolio should be almost effortless.

My workflow:

```text
Build something
     ↓
Create GitHub repository
     ↓
Push code
     ↓
Add description/topics
     ↓
Add live demo if available
     ↓
Done
```

The portfolio handles the rest.

```text
GitHub
   ↓
Fetch repository
   ↓
Process project data
   ↓
Display project
```

---

## Why I built it this way

I build a lot of small projects, experiments, websites, and apps.

The problem with a traditional portfolio is that the portfolio itself becomes another project that needs maintenance.

Every time I create something new, I have to remember to update it.

Using GitHub as the source of project data removes most of that work.

I can focus on building projects and keeping my GitHub repositories organized, while the portfolio takes care of showcasing them.

---

## Future ideas

Some things I'd like to add later:

* GitHub contribution graph
* Recent GitHub activity
* Automatic project screenshots
* Deployment status
* Commit statistics
* Star history
* Project search
* Better project categorization
* Automatic README previews
* GitHub Actions integration
* Automatic detection of Vercel/Netlify deployments

---

## Final idea

The whole project comes down to one principle:

> **I maintain my GitHub, and my portfolio maintains itself.**

Instead of manually updating a portfolio whenever I build something new, I can simply keep building and pushing projects to GitHub.
