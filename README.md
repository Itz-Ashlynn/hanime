# Hanime API (Cloudflare Worker)

This API is a serverless implementation of a Hanime-related service, running on Cloudflare Workers. It provides various endpoints to fetch trending videos, browse categories, and retrieve video details in a structured JSON format.

## Table of Contents

1. [Features](#features)
2. [Endpoints](#endpoints)
   - [`GET /`](#get-)
   - [`GET /watch/:slug`](#get-watchslug)
   - [`GET /trending/:time/:page`](#get-trendingtimepage)
   - [`GET /browse/:type`](#get-browsetype)
   - [`GET /tags`](#get-tags)
   - [`GET /:type/:category/:page`](#get-typecategorypage)
3. [Example Usage](#example-usage)
4. [Error Handling](#error-handling)

---

## Features

- Fetch trending videos based on time and page.
- Retrieve detailed video information using a unique slug.
- Browse categories such as hentai tags and brands.
- Supports pagination for seamless data exploration.

---

## Endpoints

### `GET /`

**Description:**
Returns a welcome message to indicate the API is operational.

**Example Request:**

```bash
curl -X GET https://your-api-url.com/
```

**Example Response:**

```plaintext
Welcome to Hanime API 👀
```

---

### `GET /watch/:slug`

**Description:**
Fetches detailed information about a specific video using its slug.

**Parameters:**

- `slug` (string): The unique identifier for the video.

**Example Request:**

```bash
curl -X GET https://your-api-url.com/watch/some-video-slug
```

**Example Response:**

```json
{
  "results": [
    {
      "id": 123,
      "name": "Video Name",
      "description": "A detailed description of the video.",
      "poster_url": "https://example.com/poster.jpg",
      "cover_url": "https://example.com/cover.jpg",
      "views": 1000,
      "streams": [
        { "width": 1920, "height": 1080, "size_mbs": 500, "url": "https://example.com/video.mp4" }
      ],
      "tags": [
        { "name": "Tag1", "link": "/hentai-tags/Tag1/0" }
      ],
      "episodes": []
    }
  ]
}
```

---

### `GET /trending/:time/:page`

**Description:**
Fetches trending videos based on the specified time range and page number.

**Parameters:**

- `time` (string): The time filter (e.g., `day`, `week`, `month`).
- `page` (integer): The page number to fetch.

**Example Request:**

```bash
curl -X GET https://your-api-url.com/trending/week/1
```

**Example Response:**

```json
{
  "results": [
    {
      "id": 123,
      "name": "Trending Video",
      "slug": "trending-video",
      "cover_url": "https://example.com/cover.jpg",
      "views": 1500,
      "link": "/watch/trending-video"
    }
  ],
  "next_page": "/trending/week/2"
}
```

---

### `GET /browse/:type`

**Description:**
Fetches browsing data for a specific type (e.g., hentai tags, brands).

**Parameters:**

- `type` (string): The category to browse (e.g., `hentai_tags`, `brands`).

**Example Request:**

```bash
curl -X GET https://your-api-url.com/bi
```

** iExample Response:**

```json
{
  "results": [
    { "text": "Tag1", "url": "/hentai-tags/Tag1/0" }
  ]
}
```

---

### `GET /tags`

**Description:**
Fetches all available hentai tags.

**Example Request:**

```bash
curl -X GET https://your-api-url.com/tags
```

**Example Response:**

```json
{
  "results": [
    { "text": "Tag1", "url": "/tags/Tag1/0" }
  ]
}
```

---

### `GET /:type/:category/:page`

**Description:**
Fetches videos from a specific category and type, paginated by the page number.

**Parameters:**

- `type` (string): The type of videos (e.g., `hentai_videos`).
- `category` (string): The category slug.
- `page` (integer): The page number to fetch.

**Example Request:**

```bash
curl -X GET https://your-api-url.com/hentai_videos/category_slug/1
```

**Example Response:**

```json
{
  "results": [
    {
      "id": 456,
      "name": "Category Video",
      "slug": "category-video",
      "cover_url": "https://example.com/cover.jpg",
      "views": 2000,
      "link": "/watch/category-video"
    }
  ],
  "next_page": "/hentai_videos/category_slug/2"
}
```

---

## Example Usage

### Using `curl`

You can test the API endpoints directly using `curl` as shown in the examples above.

### Using JavaScript Fetch

```javascript
fetch('https://your-api-url.com/trending/week/1')
  .then(response => response.json())
  .then(data => console.log(data));
```

---

## Error Handling

In case of errors, the API responds with a JSON object containing the error message:

**Example Error Response:**

```json
{
  "error": "Something went wrong"
}
```

**HTTP Status Codes:**

- `200 OK`: Successful request.
- `404 Not Found`: Endpoint not found.
- `500 Internal Server Error`: Server encountered an error.

---

## Contributing

Feel free to contribute by submitting issues or pull requests on GitHub. Make sure to follow best practices and provide clear descriptions for changes.

---

## License

This project is licensed under the MIT License.

