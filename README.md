# The Rockers - DevOps Practice

This is a simple Go web application for "The Rockers" band website. It serves static HTML pages for Home, About, Schedule, and Contact, along with static assets like CSS and images.

## Features

- Static website with multiple pages (Home, About, Schedule, Contact)
- Styled with custom CSS
- Dockerized for easy deployment

## Getting Started

### Prerequisites

- [Go](https://golang.org/dl/) 1.22 or higher
- [Docker](https://www.docker.com/) (optional, for containerized runs)

### Clone the Repository

```sh
git clone https://github.com/Omayer111/TheRockers-DevOps-Practice.git
cd TheRockers-DevOps-Practice
```

### Run Locally (without Docker)

```sh
go run main.go
```

Visit [http://localhost:8080](http://localhost:8080) in your browser.

### Run with Docker

Build and run the container:

```sh
docker build -t therockers-app .
docker run -p 8080:8080 therockers-app
```

Visit [http://localhost:8080](http://localhost:8080) in your browser.

## Project Structure

```
.
├── main.go             # Main Go application
├── main_test.go        # Unit tests
├── go.mod              # Go module file
├── Dockerfile          # Docker build instructions
├── static/             # Static assets (HTML, CSS, images)
│   ├── about.html
│   ├── contact.html
│   ├── home.html
│   ├── schedule.html
│   ├── style.css
│   └── images/
│       ├── golang-website.png
│       └── rock-concert.jpg
└── README.md
```

## Testing

Run unit tests with:

```sh
go test
```

## License

This project is for educational purposes.
inspired by Abhishek Veeramalla