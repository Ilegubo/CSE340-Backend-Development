# Project Notes and Lessons Learned

## Project Overview
This project is a basic Express application for serving pages for a home page, organizations page, and projects page. The app uses EJS templates and serves static assets from the public folder.

## Steps Taken to Complete the Project
1. Initialize the project and install dependencies.
   - Express was installed for the server.
   - EJS was installed for template rendering.
   - Nodemon was installed for development.

2. Set up the server entry file.
   - The app was created with `express()`.
   - The port was configured using `process.env.PORT || 3000`.
   - The project root was determined using `__dirname` and `fileURLToPath()`.

3. Configure Express middleware.
   - Static files were served from the `public` folder.
   - Template rendering was configured for EJS.

4. Create view templates.
   - Files were placed in the `src/views` directory.
   - Template names matched the route names used in the server.

5. Define routes.
   - `/` renders the home page.
   - `/organizations` renders the organizations page.
   - `/projects` renders the projects page.

6. Start the server.
   - The app was run with `npm run dev` or `npm start`.
   - The browser was opened on the local development URL.

## Important Points to Remember
- Express needs a template engine configured before calling `res.render()`.
- If using EJS, the app must include:
  `app.set('view engine', 'ejs');`
  `app.set('views', path.join(__dirname, 'src/views'));`
- Route names must match the actual template filenames.
- Files in `src/views` are not `.html` files unless the project is specifically built for raw HTML delivery.
- Static files such as CSS and images belong in the `public` folder.
- `res.sendFile()` is for serving files directly, while `res.render()` is for rendering template pages.

## Errors Made and Lessons Learned
### 1. Wrong file extension in the routes
Problem:
The routes attempted to serve `home.html`, `organizations.html`, and `projects.html`, but the actual files were `.ejs` files.

Why it happened:
The project used EJS, but the route paths still referenced HTML files.

Lesson:
Always check the actual files in the `src/views` directory before writing route paths.

### 2. Missing EJS engine configuration
Problem:
The app threw:
`Error: No default engine was specified and no extension was provided.`

Why it happened:
The app called `res.render()` without setting the view engine.

Lesson:
Always configure the view engine before route rendering:
`app.set('view engine', 'ejs');`
`app.set('views', path.join(__dirname, 'src/views'));`

### 3. Browser trying to download the page instead of rendering it
Problem:
The browser prompted to download a file instead of showing the page.

Why it happened:
The route was serving a file path incorrectly or using the wrong type of response.

Lesson:
Use `res.render()` for EJS pages and `res.sendFile()` only when serving real files that exist and should be downloaded or displayed as files.

### 4. Not verifying the project structure before route setup
Problem:
The wrong folder/file assumptions caused repeated errors.

Lesson:
Before writing routes, list the actual project folders and files so the path matches the real structure.

## Best Practices for Future Work
- Confirm the actual file structure before building routes.
- Match route names with template names exactly.
- Set the view engine before rendering templates.
- Use the correct Express method:
  - `res.render()` for views
  - `res.sendFile()` for direct file delivery
- Keep static assets in `public` and templates in `src/views`.
- Test with `npm run dev` after each major change.

## Final Reminder
When working with Express and EJS, the quickest way to avoid errors is:
1. Confirm the template files exist.
2. Configure the view engine.
3. Render the right template name.
4. Make sure the route and file names match.
5. Test the app after each fix.
