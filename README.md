# TcMenu framework Documentation

This contains the library docs as found on theCodersCorner website. 

This site uses the layout of our internal systems, it converts markdown to HTML and then uses a custom spring boot and freemarker application to serve the pages.

To develop the site just load the directory into an editor such as VS Code or IntelliJ. You can use most regular markdown conventions, including fenced code blocks and tables.

## Building the ref-docs documentation

Generally speaking, there is a link to the reference (or doxygen generated) documents within the site, these are usually hosted at the `/ref-docs` location and each of the library repositories and the tcMenu API are built in turn to this end. These are built on web server as the documentation changes.

## A few basic rules for committers

Avoid breaking links at all costs, do not refactor page names or positions without talking to one of the committers first. Check your spelling is correct, best to use a spell checker in the editor that you are using. Think about others needing to read your text, make it as short as you can while keeping the meaning.

If you are adding a new page, or making more than a small correction or readabilty/style change, then please reach out to us first to avoid wasted time later explaining the purpose of the change.

# License and Terms of Use

## 1. Content License

The text and media content of this documentation are licensed under the [Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International (CC BY-NC-ND 4.0) license](https://creativecommons.org/licenses/by-nc-nd/4.0/legalcode).

What this means:

* Attribution: You must give appropriate credit and provide a link to the original source at thecoderscorner.com.
* Non-Commercial: You may not use this material for commercial purposes.
* NoDerivatives: If you remix, transform, or build upon the material, you may not distribute the modified material without explicit permission.

## 2. Branding and Trademarks

The TheCodersCorner name, the tcMenu name, and all associated logos are trademarks. This license does not grant you any rights to use these trademarks for your own hosting or products.

## 3. External Hosting Policy

* We strongly prefer that you do not host a mirror of this site. Fragmented documentation leads to outdated information which confuses the community. If you have a specific need to host this content externally:

* Please contact us first to discuss your requirements.
* Canonical Links: Any hosted version must include a <link rel="canonical" href="..."> tag on every page pointing back to the official documentation on thecoderscorner.com to preserve search engine integrity.
* De-branding: You must remove all TheCodersCorner logos and branding, replacing them with your own.