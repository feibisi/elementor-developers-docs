---
title: "License Deactivation"
post_status: publish
comment_status: open
taxonomy:
  category:
    - elementor-developers-docs
  post_tag:
    - Cli
    - Src
    - Repos
---

# License Deactivation

<Badge type="tip" vertical="top" text="Elementor Pro" /> <Badge type="warning" vertical="top" text="Advanced" />

Some Elementor Pro licenses can activate multiple sites. If no more activations are left on a license, you can deactivate some sites to free up more activations. You can deactivate a site from the admin panel or from the command line using the `license deactivate` command.

## Command

```bash
wp elementor-pro license deactivate
```

## Arguments

None.

## Usage Examples

```bash
wp elementor-pro license deactivate
```

This command will deactivate a site's Elementor Pro license.