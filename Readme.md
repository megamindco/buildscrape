# Build Scrape

This project is a simple Flask-based web scraper API that allows you to extract and summarize content from any website. It uses BeautifulSoup to parse and extract text and headers from a webpage, with optional summarization functionality.

## Features

- Scrape full webpage content, including text and headings (`<h1>`).
- Optional summarization of the content.
- Bearer token-based authentication for security.
- Rate-limiting to control API usage.
- Containerized using Docker for easy deployment.

## Table of Contents

- [Build Scrape](#build-scrape)
  - [Features](#features)
  - [Table of Contents](#table-of-contents)
  - [Installation](#installation)
  - [Usage](#usage)
    - [API Endpoints](#api-endpoints)
      - [`GET /scrape`](#get-scrape)
  - [Docker](#docker)
  - [Environment Variables](#environment-variables)
  - [Contributing](#contributing)
    - [Steps to Contribute:](#steps-to-contribute)
  - [License](#license)

## Installation

To run this project locally, follow these steps:

1. Clone this repository:

   ```bash
   git clone https://github.com/tiwarihardik/buildscrape.git
   cd buildscrape
   ```

2. Set up a Python virtual environment and install dependencies:

   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows use `venv\Scripts\activate`
   pip install -r requirements.txt
   ```

3. Create a `.env` file in the root directory and add your **Bearer Token** or simply rename `.env.example ` and add your token:

   ```bash
   BEARER_TOKEN=your_bearer_token_here
   ```

4. Run the Flask application:

   ```bash
   python app.py
   ```

   The server will be accessible at `http://localhost:5000`.

## Usage

You can use the Flask web scraper API to scrape content from any website by sending a **GET** request to the `/scrape` endpoint.

### API Endpoints

#### `GET /scrape`

Scrape content from a given URL.

**Parameters:**
- `url` (required): The URL of the website to scrape.
- `summarize` (optional): Set to `true` to get a summarized version of the content.

**Headers:**
- `Authorization`: Include a Bearer token for authentication.
  - Example: `Authorization: Bearer YOUR_BEARER_TOKEN`

**Example Request:**
```bash
curl -X GET "http://localhost:5000/scrape?url=http://example.com&summarize=true" -H "Authorization: Bearer your_bearer_token_here"
```

**Response:**
```json
{
  "headings": ["Heading 1", "Heading 2", "Heading 3"],
  "content": "Summarized or full content of the webpage..."
}
```

## Docker

This project is containerized using Docker. To run it in a Docker container:

1. **Build the Docker image:**

   ```bash
   docker build -t buildscrape .
   ```
   or 
   
   ```bash
   ./build.sh
   ```

2. **Run the Docker container:**

   ```bash
   docker run -p 5000:5000 --env-file .env flask-web-scraper
   ```
   or 
   
   ```bash
   ./start.sh
   ```

3. **Access the application:**

   The application will be available at `http://localhost:5000`.

## Environment Variables

Make sure to define the following environment variables in your `.env` file:

- **BEARER_TOKEN**: Your secret Bearer token for authentication.

Example `.env` file:
```bash
BEARER_TOKEN=your_bearer_token_here
```

## Contributing

We welcome contributions! If you find a bug or want to add a feature, feel free to open an issue or a pull request.

### Steps to Contribute:
1. Fork the repository.
2. Create a new branch (`git checkout -b feature-branch`).
3. Commit your changes (`git commit -am 'Add new feature'`).
4. Push to the branch (`git push origin feature-branch`).
5. Open a pull request.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
