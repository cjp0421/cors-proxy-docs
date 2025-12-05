# Go + AWS Lambda CORS Proxy — Documentation Site

![Hugo](https://img.shields.io/badge/Hugo-Docs-blueviolet)
![AWS Lambda](https://img.shields.io/badge/AWS-Lambda-orange)
![Go](https://img.shields.io/badge/Go-1.22+-blue)
![Status](https://img.shields.io/badge/Purpose-Portfolio-lightgrey)

This repository contains the Hugo documentation site for a small, focused guide I wrote on
**using a minimal Go AWS Lambda proxy to work around CORS issues.**

The goal of this project is simple:
to explain this pattern clearly, with no backend expertise required, and to create a polished documentation artifact for my own portfolio and reference.

This repo is not intended for collaboration or external edits.

---

## Running the Docs Locally

If you want to view the site locally:

```bash
hugo server -D
```

Then open:

```
http://localhost:1313/
```

The site will reload on changes automatically.

---

## Project Structure

This is a standard Hugo project.  
Here’s where everything lives:

```
./
├── content/               # All documentation pages
│   ├── _index.md          # Docs homepage
│   ├── overview/          # What problem this solves
│   ├── cors/              # What CORS is, short and simple
│   ├── prerequisites/     # What you need beforehand
│   ├── architecture/      # High-level flow
│   ├── lambda/            # Creating the Lambda
│   ├── handler/           # Go handler explanation
│   ├── api-gateway/       # Connect Lambda to API Gateway
│   ├── testing/           # Smoke tests + debugging
│   ├── security/          # What’s safe, what to watch for
│   ├── appendix/          # Extras if needed
│   └── images/            # Images used in the docs
│
├── themes/
│   └── hugo-theme-techdoc # Local copy of the theme
│
├── static/                # Custom CSS/assets
├── layouts/               # Any template overrides
│
├── config.toml            # Hugo configuration
└── README.md              # This file
```

---

## Purpose of This Repo

This is a **personal documentation project**, created to:

- Demonstrate clear technical writing  
- Explain a common frontend problem (CORS)  
- Show how to build a simple Lambda proxy in Go  
- Build a full docs site using Hugo  
- Provide a resource I can reference or share in my portfolio  

---

## License

MIT
