#  Jekyll + GitHub Pages + Other Hosting

Jekyll requires hard-coding an absolute URL, so it doesn't support "build once, deploy everywhere." However, it can be built repeatedly with small changes for each deployment location.

This is a basic example of how to simultaneously deploy a Jekyll site to 2 different locations:
1. Using the new standard for a GitHub Pages build and deploy flow
2. Using a deploy branch that can be connected to "other" hosting, with a different URL

## Steps

1. Create a new GitHub Pages project repo
    - Settings > Pages > Build and deployment > Source: `GitHub Actions`
    - Do **not** choose to use/add the `Jekyll` workflow if suggested/prompted, leave it blank
2. Build out Jekyll project for GitHub Pages as normal (see `_config.yml`, `Gemfile`)
3. Add the workflow file to the project, copied from `.github/workflows/build-and-deploy.yml`
4. Update the `env` variables as needed:
    - **RUBY_VERSION:** The Ruby version to use
    - **OTHER_HOSTING_URL:** The URL for the site on Other Hosting (e.g., "https://mysite.myunit.gatech.edu")
    - **OTHER_HOSTING_BASEURL:** The base URL for the site on Other Hosting (e.g., "/blog")
    - **OTHER_HOSTING_BRANCH:** The deployment branch for the site build files for Other Hosting
5. Commit to project repo and trigger the build process

The results should both deploy the site to GitHub Actions, as well as create a branch that another hosting service can consume. Alternatively, the workflow could be modified to transfer the build files more directly (e.g., SSH, SFTP, S3 upload, etc.).

**Notes:** 
- This is a rough proof-of-concept solution to satisfy a possible requirement for dual hosting + domain names.
- Hosting the same site with two different URLs has SEO implications.
- Jekyll themes can introduce different config requirements: if your build step is failing due to a missing value, make sure to add it in your `_config.yml`.