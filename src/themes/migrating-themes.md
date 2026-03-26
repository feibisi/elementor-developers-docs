---
title: "Migrating Themes"
post_status: publish
comment_status: open
taxonomy:
  category:
    - elementor-developers-docs
  post_tag:
    - Themes
    - Src
    - Repos
---

# Migrating Themes

<Badge type="tip" vertical="top" text="Elementor Pro" /> <Badge type="warning" vertical="top" text="Intermediate" />

Now we'll see how to support Elementor theme locations in your theme. The logic behind the process is simple, you just need to wrap your code with an Elementor function/hook that checks to see if the user prefers using the Elementor template or the original theme design.

There are two ways to support Elementor locations - you can either use custom Elementor _functions_ or _hooks_. Both ways will work. With hooks, the entire logic is in the `functions.php` file. With functions, the checks are inside the theme files.

## Live Example

In the following, we'll look at some examples of theme migration:

* [Original Theme](src/themes/original-theme)
* [Migrating Themes with Functions](src/themes/migrating-themes-with-hooks)
* [Migrating Themes with Hooks](src/themes/migrating-themes-with-functions)