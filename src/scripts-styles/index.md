---
title: "Scripts & Styles"
post_status: publish
comment_status: open
taxonomy:
  category:
    - elementor-developers-docs
  post_tag:
    - Scripts Styles
    - Src
    - Repos
---

# Scripts & Styles

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Intermediate" />

Just like WordPress, Elementor has special hooks to register custom scripts and styles. It's very important to use the correct hook in order to improve site performance. Using Elementor recommendations and best practices helps Elementor enqueue files dynamically only when they are used, reducing performance impact.

## Static vs. Dynamic Loading

Some scripts should always be loaded, others only when used. For example, editor scripts should always be loaded, while widget scripts should only be loaded when they are being used. Elementor allows developers the freedom of choosing either method. 

Each script and stylesheet increases the page size. This is why it is best practice to register assets and let Elementor decide whether or not to load them. Elementor checks to see if the page uses an element requiring your script, and only then it is loaded.

## Frontend Scripts & Styles

Learn more about registering new scripts and styles to frontend pages:

* [Frontend Scripts](src/scripts-styles/frontend-scripts)
* [Frontend Styles](src/scripts-styles/frontend-styles)

## Editor Scripts & Styles

Learn more about registering new scripts and styles to the [Elementor Editor](src/editor/elementor-panel):

* [Editor Scripts](src/scripts-styles/editor-scripts)
* [Editor Styles](src/scripts-styles/editor-styles)

## Preview Scripts & Styles

Learn more about registering new scripts and styles to [Elementor preview](src/editor/elementor-preview):

* [Preview Scripts](src/scripts-styles/preview-scripts)
* [Preview Styles](src/scripts-styles/preview-styles)

## Widget Scripts & Styles

Learn more about registering custom scripts and styles to [Elementor widgets](src/widgets):

* [Widget Scripts](src/scripts-styles/widget-scripts)
* [Widget Styles](src/scripts-styles/widget-styles)

## Controls Scripts & Styles

Learn more about registering custom scripts and styles to [Elementor controls](src/controls):

* [Control Scripts](src/scripts-styles/control-scripts)
* [Control Styles](src/scripts-styles/control-styles)