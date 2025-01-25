
# Setup Guide for Advanced Features using Jekyll, GitHub Actions, and Django

This guide will help you set up advanced features like **Jekyll**, **GitHub Actions**, and **Django** using **MacBook**. It will include step-by-step instructions and tips to integrate these technologies with your GitHub repository.

---

## Table of Contents
1. [Installing Jekyll on macOS](#1-installing-jekyll-on-macos)
2. [Creating and Deploying a Jekyll Website](#2-creating-and-deploying-a-jekyll-website)
3. [Setting up GitHub Actions for Automation](#3-setting-up-github-actions-for-automation)
4. [Setting up Django on macOS](#4-setting-up-django-on-macos)
5. [Deploying Django App to GitHub Pages (Optional)](#5-deploying-django-app-to-github-pages-optional)
6. [Troubleshooting](#6-troubleshooting)
7. [Conclusion](#7-conclusion)

---

## 1. Installing Jekyll on macOS

Jekyll is a static site generator that allows you to create blogs, portfolios, and websites. It integrates seamlessly with GitHub Pages.

### Steps to Install:

1. **Install Homebrew** (if you don't have it yet):
   - Open **Terminal** and run:
     ```bash
     /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
     ```

2. **Install Ruby**:
   - Run:
     ```bash
     brew install ruby
     ```
   - Add Ruby to your path:
     ```bash
     echo 'export PATH="/opt/homebrew/opt/ruby/bin:$PATH"' >> ~/.zshrc
     source ~/.zshrc
     ```

3. **Install Jekyll and Bundler**:
   - Run:
     ```bash
     gem install --user-install bundler jekyll
     ```

4. **Verify Installation**:
   - Check that Jekyll is installed:
     ```bash
     jekyll -v
     ```

---

## 2. Creating and Deploying a Jekyll Website

Once Jekyll is installed, you can create a new Jekyll website and deploy it to GitHub Pages.

### Steps to Create and Deploy:

1. **Create a New Jekyll Site**:
   - Navigate to the directory where you want to create the site:
     ```bash
     cd ~/Sites
     ```
   - Run the following command:
     ```bash
     jekyll new my-website
     ```
   - Navigate to your project folder:
     ```bash
     cd my-website
     ```

2. **Preview the Site Locally**:
   - Run:
     ```bash
     bundle exec jekyll serve
     ```
   - Visit `http://localhost:4000` in your browser to preview the site.

3. **Push to GitHub**:
   - Initialize a Git repository:
     ```bash
     git init
     git add .
     git commit -m "Initial Jekyll site commit"
     ```
   - Create a GitHub repository (e.g., `my-website`).
   - Add the remote and push:
     ```bash
     git remote add origin https://github.com/your-username/my-website.git
     git push -u origin master
     ```

4. **Enable GitHub Pages**:
   - Go to your GitHub repository’s **Settings > Pages**.
   - Set the source to the `master` branch (or `main`).
   - Your Jekyll site is now live at `https://your-username.github.io/my-website/`.

---

## 3. Setting up GitHub Actions for Automation

GitHub Actions is a CI/CD tool that automates workflows directly in your GitHub repository.

### Steps to Create a Workflow:

1. **Create a Workflow File**:
   - Inside your repository, create a `.github/workflows` folder.
   - In this folder, create a file called `deploy.yml`.

2. **Sample Workflow for Deploying Jekyll Site**:

   ```yaml
   name: Deploy Jekyll Site to GitHub Pages

   on:
     push:
       branches:
         - main  # Trigger on pushes to the 'main' branch

   jobs:
     deploy:
       runs-on: ubuntu-latest
       steps:
         - name: Checkout repository
           uses: actions/checkout@v2

         - name: Setup Ruby and Jekyll
           uses: ruby/setup-ruby@v1
           with:
             ruby-version: '2.7'

         - name: Install dependencies
           run: |
             gem install bundler
             bundle install

         - name: Build the Jekyll site
           run: |
             bundle exec jekyll build

         - name: Deploy to GitHub Pages
           uses: peaceiris/actions-gh-pages@v3
           with:
             github_token: ${{ secrets.GITHUB_TOKEN }}
             publish_dir: ./_site
   ```

3. **Push Changes**:
   - Commit and push the changes to your repository:
     ```bash
     git add .
     git commit -m "Add GitHub Actions workflow"
     git push origin main
     ```

4. **Check the Action**:
   - Visit your **Actions** tab on GitHub to see the status of the workflow.

---

## 4. Setting up Django on macOS

If you prefer dynamic websites, Django is a powerful web framework. Here’s how to set it up.

### Steps to Install Django:

1. **Install Python** (if not already installed):
   - Django requires Python. If you don't have it installed, install it from the [official website](https://www.python.org/downloads/).

2. **Install Django**:
   - Open **Terminal** and run:
     ```bash
     pip install django
     ```

3. **Create a New Django Project**:
   - Navigate to your projects directory:
     ```bash
     cd ~/Sites
     ```
   - Run:
     ```bash
     django-admin startproject mysite
     cd mysite
     ```

4. **Run the Development Server**:
   - Run:
     ```bash
     python manage.py runserver
     ```
   - Visit `http://127.0.0.1:8000/` to view your Django site.

---

## 5. Deploying Django App to GitHub Pages (Optional)

Django applications are dynamic, which means GitHub Pages isn’t suitable for direct deployment. However, you can deploy Django using platforms like **Heroku** or **Vercel**.

### Steps to Deploy with Heroku:

1. **Install Heroku CLI**:
   - Download and install Heroku CLI from [here](https://devcenter.heroku.com/articles/heroku-cli).

2. **Create a `Procfile`**:
   - In the root of your Django project, create a file called `Procfile` and add:
     ```
     web: gunicorn mysite.wsgi
     ```

3. **Add Gunicorn**:
   - Run:
     ```bash
     pip install gunicorn
     ```

4. **Create a Heroku App**:
   - Log in to Heroku using `heroku login` in the terminal.
   - Create a new Heroku app:
     ```bash
     heroku create my-django-app
     ```

5. **Push to Heroku**:
   - Add, commit, and push the code to Heroku:
     ```bash
     git add .
     git commit -m "Deploy Django to Heroku"
     git push heroku master
     ```

6. **Visit Your App**:
   - After deployment, visit your Heroku app at `https://my-django-app.herokuapp.com/`.

---

## 6. Troubleshooting

### Common Issues:
- **GitHub Actions Workflow Not Triggering**:
   - Ensure you’re pushing to the correct branch (e.g., `main`).
   - Check if the `.github/workflows` directory exists and contains the `.yml` file.

- **Django Not Running**:
   - Ensure all dependencies are installed (`pip install -r requirements.txt`).
   - Check if your database is correctly configured and migrated (`python manage.py migrate`).

- **Git Push Issues**:
   - Ensure you have the correct remote set up (`git remote -v`).

---

## 7. Conclusion

You now have a full guide to set up **Jekyll**, **GitHub Actions**, and **Django** on your **MacBook**, as well as deploying them to **GitHub Pages** (for static sites) or **Heroku** (for dynamic Django apps). Automate your deployment with **GitHub Actions** and streamline your workflow.

Feel free to extend and modify the repository as needed!

