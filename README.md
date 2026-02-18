
## Usage

1. Go to [convert.to.it](https://convert.to.it/)
2. Click the big blue box to add your file (or just drag it on to the window).
3. An input format should have been automatically selected. If it wasn't, yikes! Try searching for it, or if it's really not there, see the "Issues" section below.
4. Select an output format from the second list. If you're on desktop, that's the one on the right side. If you're on mobile, it'll be somewhere lower down.
5. Click **Convert**!
6. Hopefully, after a bit (or a lot) of thinking, the program will spit out the file you wanted. If not, see the "Issues" section below.


## Deployment

### Local development (Bun + Vite)

1. Clone this repository ***WITH SUBMODULES***. You can use `git clone --recursive https://github.com/p2r3/convert` for that. Omitting submodules will leave you missing a few dependencies.
2. Install [Bun](https://bun.sh/).
3. Run `bun install` to install dependencies.
4. Run `bunx vite` to start the development server.

_The following steps are optional, but recommended for performance:_

When you first open the page, it'll take a while to generate the list of supported formats for each tool. If you open the console, you'll see it complaining a bunch about missing caches.

After this is done (indicated by a `Built initial format list` message in the console), use `printSupportedFormatCache()` to get a JSON string with the cache data. You can then save this string to `cache.json` to skip that loading screen on startup.

### Docker (prebuilt image)

Docker compose files live in the `docker/` directory, so run compose with `-f` from the repository root:

```bash
docker compose -f docker/docker-compose.yml up -d
```

Alternatively download the `docker-compose.yml` separately and start it by executing `docker compose up -d` in the same directory.

This runs the container on `http://localhost:8080/convert/`.

### Docker (local build for development)

Use the override file to build the image locally:

```bash
docker compose -f docker/docker-compose.yml -f docker/docker-compose.override.yml up --build -d
```

The first Docker build is expected to be slow because Chromium and related system packages are installed in the build stage (needed for puppeteer in `buildCache.js`). Later builds are usually much faster due to Docker layer caching.

