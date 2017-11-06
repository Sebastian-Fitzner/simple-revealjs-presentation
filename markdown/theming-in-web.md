# Theming Approaches

--

## Sitemap

1. Introduction
1. VWN Theming
1. Migros Theming
1. Asklepios Theming

---

# Introduction

--

## Frameworks

--

## DO not invent the wheel...

--

**... when it is not necessary!**

![alt Invent it](https://media.giphy.com/media/92Azfn0WSfpHa/giphy.gif "Invent it")

--

Just take a look at Bootstrap, Foundation or other SCSS frameworks to get a starting point.

---

# VWN Theming (Veams Theming)

--

## Requirements

1. Multiple landing pages with same components
1. Different themes per landing page

--

## Setup

1. For each component we created one repository
1. Each component is completely self-contained
1. Each component exposes theming variables

--

## Usage

1. In the landing page project we required the component as submodule.
1. Specific styles are applied via `id` and overrides generic elements.

---

# Migros Theming

---

# Asklepios Theming