---
layout: post
title: 'Managing Jekyll Configurations for Local and GitHub Deployment'
date: 2023-08-03 10:00:00 -0700
categories: [Blog, Technology, Jekyll, Git]
author: Sean Morrison
---

**Problem**: Switching between local and GitHub configurations was a tedious process involving manual commenting and uncommenting of the configuration parameters.

**Old Approach**:

- Commenting out local configuration when pushing to GitHub.
- Commenting out GitHub configuration when running locally.

**New Solution**:

1. **Keep the Default Configuration**: In your `_config.yml` file, leave the GitHub configuration active, and comment out the local configuration.

2. **Create a Development Configuration File**: Make another file named `_config_dev.yml` and put the local configuration in there, uncommented.

3. **Run Locally with Both Configurations**: When you want to run your Jekyll site locally, use the following command:

   ```bash
   bundle exec jekyll serve --config _config.yml,_config_dev.yml
   ```

   This command tells Jekyll to load both configuration files, with values in `_config_dev.yml` taking precedence. It means you can keep your production settings in `_config.yml`, and your local development overrides in `_config_dev.yml`.

4. **Push Updates as Usual**: When you push an update, the default `_config.yml` file will be used, so your GitHub configuration is already set.

5. **Celebrate**: You no longer have to manually comment or uncomment lines in the configuration. It's all automated, making your workflow much more streamlined and efficient. Yay!

**Benefits**:

- **Convenience**: Easily switch between configurations without manual changes.
- **Maintainability**: Separate files allow you to keep local and production configurations neatly organized.
- **Scalability**: You can further extend this approach with different configuration files for various environments or use cases.

This new approach enhances my development workflow and makes it more adaptable and less error-prone. It's a great example of using tools and best practices to optimize development processes.
