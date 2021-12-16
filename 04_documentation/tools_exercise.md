# Writing and Publishing Documentation

This exercise is about documentation of projects and codes. We have already added documentation to the [corresponding repository](https://github.com/Simulation-Software-Engineering/documentation-tools-exercise). It is your task now to generate a website using [MkDocs](https://www.mkdocs.org/getting-started/) and to deploy it to [GitHub Pages](https://pages.github.com/).

At the end of the exercise you find a section with hints and remarks. Make sure to check this section.

Deadline: **Thursday, January 13th, 2022, 9:00**

## Documentation Publication Steps

- Create a new repository named "sse-mkdocs-exercise" on GitHub in you own account/namespace on GitHub and clone the repository afterwards.

  **Note**: In this exercise you **cannot work with forks** because you cannot use GitHub Pages with forks. It is also easier to deploy the website if your account is the owner of the repository.
- Add the contents of the [`documentation-tools-exercise` repository](https://github.com/Simulation-Software-Engineering/documentation-tools-exercise) to your own repository. You can do this by copying the files into your own repository, adding and commiting them to Git. Afterwards push the changes to GitHub and verify that your repository contains the same files as the `documentation-tools-exercise` repository.

  **Note**: If you use another way of adding the data to your repository, e.g., by defining a new remote, make sure that the `origin` remote points to your own repository. Otherwise, the deployment step below will push the website to the wrong repository.
- Follow the instructions from the [MkDocs homepage](https://www.mkdocs.org/getting-started/) to install MkDocs.
- [Create a MkDocs project](https://www.mkdocs.org/getting-started/#creating-a-new-project) from the root of the repository via

  ```bash
  mkdocs new .
  ```

  This will create a MkDocs configuration file `mkdocs.yml` in the root of the repository and a file `index.md` in the `docs/` directory. Make sure to add these new files to Git.

- Create the documentation website locally by running `mkdocs serve`. This builds the homepage and runs a local web server. It will also look for changes to the Markdown files and the `mkdocs.yml` file while it is running to rebuild the website. `mkdocs serve` should print something like the following on the screen

  ```bash
  mkdocs serve
  INFO     -  Building documentation...
  INFO     -  Cleaning site directory
  INFO     -  Documentation built in 0.07 seconds
  INFO     -  [10:43:37] Serving on http://127.0.0.1:8000/
  ```

  Copy the address mentioned after "Serving on", in this example `http://127.0.0.1:8000/`, into your favorite browser. A website called "Welcome to MkDocs" should appear that looks similar to the example from the [MkDocs documentation (see below)](https://www.mkdocs.org/getting-started/#creating-a-new-project)

  ![Screenshot from MkDocs Getting Started guide](https://www.mkdocs.org/img/screenshot.png)

  MkDocs should identify our Markdown files inside `docs/` automatically and include them in the generated website. This means that you should find three items in the navigation bar (blue bar at the top) named `Welcome to MkDocs`, `Compilation and Installation` and `How to use the Program`. The names are generated by the top level header of the Markdown files.

  **Note**: If you are using MkDocs inside a container, you have to [forward/publish the ports to your Host](https://docs.docker.com/config/containers/container-networking/).
- Adapt the project documentation such that it the starting/index page contains information about the project. Open the `index.md` file inside the `docs` directory and replace its content with the content of the `README.md`. In contrast to Sphinx, we cannot include the `README.md` from the repository in the documentation.

  **Note**: Simply copying the content of the `REAME.md` is not a good practice. We do this in the exercise only to get meaningful content into the `index.md` quickly. One can use the `README.md` also as [index page](https://www.mkdocs.org/user-guide/writing-your-docs/#index-pages).
- [Configure the website](https://www.mkdocs.org/user-guide/configuration/) by editing the `mkdocs.yml` file. Changes made to this file might not been picked up by the interactive rebuilding of `mkdocs serve`. In this case, you have to stop `mkdocs serve` command (CTRL+C) and start it again afterwards.
    - Change the name of the website (`site_name`) from "My Docs" to "SSE Documentation Example"
    - [Add a navigation section](https://www.mkdocs.org/user-guide/writing-your-docs/#configure-pages-and-navigation) `nav` and add the three pages manually:
        - Add the `index.md` with label `Home`.
        - Create a section `User Guide` and add the following subsections.
            - Add the `compilation-and-installation.md` with label `Installation`.
            - Add the `how-to.md` with label `Getting Started`
        - You should only have two buttons "Home" and "User Guide" in the generated website.
    - Add the [repository URL](https://www.mkdocs.org/user-guide/configuration/#repo_url). This adds a "Edit on GitHub" button at the top right of the website. Try if the button works. If it does not work, this is because older versions of MkDocs set a link to the `master` branch by default, but GitHub calls this branch `main` nowadays. In order to point to the correct branch, set the `edit_uri` setting to `edit/main/docs/`.

        **Note**: The "Edit on GitHub" also fails if you have not pushed the corresponding Markdown file to your repository yet.

    - Make yourself the [website's author](https://www.mkdocs.org/user-guide/configuration/#site_author). You can use your real name or your GitHub username. This setting will not change the appearance of your website, but adds the name to the HTML metadata.
- [Deploy your website](https://www.mkdocs.org/user-guide/deploying-your-docs/) to [GitHub Pages](https://pages.github.com/). This consists of following steps:
    - Run `mkdocs gh-deploy` to build and deploy the website:

      Deployment of the website creates a branch `gh-pages` inside the repository if it does not already exist and pushes it to the default remote. The branch contains all files needed to deliver the website. You should not edit any of the files in the branch manually since `mkdocs gh-deploy` overwrites all changes. Instead, always fix problems in the main branch and deploy the website afterwards again.

    - Verify that the "Pages" feature of your repository has been activated. When you are on your repository on GitHub go to "Settings" (at top of window) -> "Pages". It should show an information box " Your site is ready to be published at URL" with the URL to the website of your documentation.

      If the "Pages" feature has not been activated automatically, choose the `gh-pages` branch as source and save/activate the website.

      Check the website. If you get a "404" error

      ```text
      404

      There isn't a GitHub Pages site here.
      ```

      wait for 5-10 minutes and try again. It takes a while for the website to become visible.

    - Add the URL of the documentation to your GitHub project. Go to your repository on GitHub and edit the "About" section at the top-right corner. For editing, click on the small gear symbol. Add the URL in the box "Website".
- Verify that your website looks as expected and that the "Edit on GitHub" feature works for all pages.
- Submit your documentation website via an issue. You cannot submit a pull request since you cannot use a fork in the exercise. You can also add the issue before you are done in order to ask questions. In that case please mention us in the issue such that we get notified. Please write a short note in the issue when you are done and the issue is ready to review. **TODO** Skip this for testing the exercise.
    - Create an issue in the [`documentation-tools-exercise` repository](https://github.com/Simulation-Software-Engineering/documentation-tools-exercise).
    - The issue should be named `[USERNAME] MkDocs exercise`, e.g., `[jaustar] MkDocs exercise`. Please use the GitLab username here.
    - Please add a link to your GitHub repository and also a link to your website in the issue.

## Optional Tasks

- [Change the theme](https://www.mkdocs.org/user-guide/choosing-your-theme/#choosing-your-theme) of your documentation. Choose either an integrated theme or a third party theme and/or configure the current scheme differently. Please mention what theme and what settings you have used.
- Add a [GitHub action](https://github.com/marketplace/actions/deploy-mkdocs) to automatically deploy your documentation every time a change is pushed to the `main` branch.
- Instead of (only) hosting the documentation on GitHub Pages we can also host the documentation on [Read the Docs](https://readthedocs.org/). You have to make sure to configure [Read the Docs](https://docs.readthedocs.io/en/stable/config-file/v2.html#mkdocs) accordingly.
- Move your documentation from MkDocs and Markdown to Sphinx and reStructuredText and host it on Read the Docs. You can follow the steps we from the lecture for this. Create a new repository on GitHub called "sse-sphinx-exercise". When you are finished with the task and/or need help, create a new issue as described above, but name the issue `[USERNAME] Sphinx exercise`.
- The code in the repository is not documented yet. Add [doxygen-style comments/doc blocks](https://www.doxygen.nl/manual/docblocks.html) to the code and generate a suitable configuration to create HTML documentation. You do not have to publish/integrate this website. Make sure that the doxygen configuration file and the documented code are part of the repository and add a screenshot of the rendered website to the issue.

## Remarks and Tips

- You do not have to compile C++ the code inside this repository at any time. This exercise is purely about documentation, documentation generation and deployment of the documentation.
- Changes to your homepage might not be immediately visible after deployment of the website. The [GitHub Pages documentation](https://docs.github.com/en/pages/getting-started-with-github-pages/creating-a-github-pages-site) also mentions this

  > It can take up to 20 minutes for changes to your site to publish after you push the changes to GitHub.

  If you do not observe any change after 60 minutes, please check whether you have actually deployed the new version of your website.