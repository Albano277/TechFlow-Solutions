# GitHub Actions Workflow Analysis

### 1. What triggers this workflow to run?

The workflow starts when changes are pushed to the `main` branch or when someone opens a pull request targeting `main`. In this assignment, I noticed that GitHub Actions ran when I created my pull requests and again after I merged them. However, the website is only deployed when changes are pushed to the `main` branch.

### 2. What are the four main steps this workflow performs?

The workflow separates testing and deployment into two jobs. First, the build-and-test job checks the HTML, examines links, and uploads the website files. Next, the deploy job uses needs: build-and-test to make sure the first job finishes successfully before deployment begins. I think this is important because it helps prevent a website from being published before the required checks are completed.

The workflow's `build-and-test` job includes four main steps:

1. **Checkout code:** Gets the project files from the repository.
2. **Validate HTML:** Checks the HTML code for errors.
3. **Check links:** Checks for broken links.
4. **Upload artifact:** Prepares and uploads the website files for deployment.

After these steps, a separate job deploys the website to GitHub Pages when the required conditions are met.

### 3. What does the "Checkout code" step do, and why is it necessary?

The Checkout code step retrieves the project files from GitHub so the workflow can work with them. This is important because GitHub Actions needs access to the files before it can check the HTML, examine links, or prepare the website for deployment. Without the files, the workflow would not be able to complete those tasks.

### 4. What is the purpose of the environment configuration?

The environment configuration tells GitHub where the website will be deployed. In this case, it uses `github-pages` and includes the website's published URL. This helps GitHub keep track of the deployment and provides a way to access the live website.

### 5. How does this automated deployment improve reliability compared to manual deployment?

Automated deployment makes the process more reliable because the same checks are performed each time changes are pushed to `main`. Instead of having to remember every step myself, GitHub Actions checks the code and handles the deployment automatically. Additionally, it can identify certain problems before the website is published. This reduces the chances of human error and makes updating the website easier and more consistent.

### 6. What would happen if you pushed code to a different branch (not main)?

If I pushed changes to another branch, such as `feature/team-section`, the workflow would not start from that push because it is configured to respond to pushes on `main`. However, opening a pull request targeting `main` would trigger the testing process. The website would not be deployed until the changes were pushed to `main` and the required checks passed.