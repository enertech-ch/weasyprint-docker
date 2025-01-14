# weasyprint

A dockerized web service for creating PDFs from HTML using WeasyPrint

## Description

[WeasyPrint](https://weasyprint.readthedocs.io/en/stable/index.html)
is a visual rendering engine for HTML and CSS that can export to PDF.
It aims to support web standards for printing.

This web service exposes an endpoint for uploading a html file, an optional css
file and optional attachments. It responds with the generated PDF.

The web service is written in Python using the aiohttp web server.

## Usage

To start the webservice just run

```
docker compose up
```

The html file and and any additional files must be uploaded as multipart/form-data
with a part named `html` containing the main HTML content. Assets (e.g. images)
that are referenced in HTML must be prefixed with `asset.`. Files that should
be attached to the generated pdf must be prefixed with `attachment.`

Example:

```
curl -F "html=@tests/index.html" -F "asset.universe.jpg=@tests/universe.jpg" http://localhost:3000 -o test.pdf
```

## Development

For development, you should clone this repo with

```
git clone https://github.com/enertech-ch/weasyprint-docker.git
```

and create a new branch.

To test your changes, you can build the image locally and start your local build with

```
docker compose build weasyprint
docker compose up weasyprint
```
