# Guidelines: Best Practices in CSS

This document is an attempt to gather information about the best practices used to create better maintainable client-side web applications.

## CSS

### Introduction / Motivation

Based on a report made through [CSS stats](www.cssstats.com), the [number of selectors in tfsports.com.br](http://cssstats.com/stats?url=http%3A%2F%2Fwww.tfsports.com.br&ua=Browser%20Default) are 10.2k as of mar/05/2018. The high number of selectors, combined with other clearly unoptimized statistics can reduce the performance of the application significantly.

Mark Otto in a report using CSS Stats as well, found out that: GitHub has around 7,000 selectors, Bootstrap has 1,900, Twitter has 8,900, Trello has 2,426, The New York Times has 2,100, and SoundCloud has 1,100.

Based in this analysis, we see the need to implement good practices regarding CSS code and architecture organization in order to improve performance and maintainability.

### The Basics

##### Airbnb CSS / Sass Styleguide  

[This styleguide](https://github.com/airbnb/css) provided by airbnb establishes useful practices to format our CSS code including commenting, identation, spacing, line-breaks, etc. You should read and follow them.

##### RSCSS - Reasonable System for CSS Stylesheet Structure

[RSCSS](http://rscss.io) is a good standard for naming, nesting, and structuring components and its elements. It considers extending, customizing and simplifying these components.

##### ITCSS

The [Inverted Triangle CSS](https://www.youtube.com/watch?v=1OKZOV-iLj4) divides the css architecture in layers from the most generic definitions to the most specific.

- Settings

  Basic configuration of your application, in general here are global variables. It won't be the final CSS.

- Tools

  The place where you will define your mixins and functions necessary to build your layouts. Fontfaces, animations, etc. Nothing here is directly generated as CSS as well.

- Generic

  Generic properties with the least specificity possible. Here we will put box-sizing, resets, etc.

- Base

  Here we will have basic styling. It's the last layer where we can put selectors directly in tags (`h1-h6, blockquote, a, button`) but all basic styling.

- Objects

  Following the principles of OOCSS (Object-oriented), here we will have our little "objects" that are chunks of the interface. In general, they have patterns that repeat across the website and can have a customized visual layer over it. Here we make the default buttons, lists, panels, etc.

- Components

  Here we will have our specific components. According to RSCSS here we will put all our components/elements. Here, instead of having generic reusable objects, we will be specific defining our components always respecting RSCSS, also not inserting positions, sizes, floats or other properties that make our component too restricted.

- Trumps

  At last we have trumps, that in RSCSS are also called helpers. This layer is responsible for the most specific declarations, even including `!important` when necessary.

###### Considerations

- Specificity will grow slowly and linearly through each layer
- We progressively add styles, we never remove them
- Each layer is more detailed and specific than the last one
- If you make a generic Object, it can be extended/reused. You should take advantage of this.
- Everything you create has its own specific place.

Booking.com also uses an extra layer called "Themes" that goes between Components and Trumps. You can use it to make quick tests in elements, colors, etc. When you put it in this place, it will have priority for its modifications.

A good explanation on ITCSS can be found in [Willian Justen's blog post on ITCSS](https://willianjusten.com.br/organizando-seu-css-com-itcss/).

### The Tools

We can define, on another moment, general tools to use in our projetcs like preprocessors, for example.

Normalizing and Sanitizing tools have to be studied and considered if needed.

### Beyond

ITCSS ("Inverted Triangle CSS") is a nice complement to any rscss structure.  
[RSCSS vs BEM](http://rscss.io/other-resources.html)

### Solution summary

- Use airbnb/css best practices for code formatting;
- Use RSCSS Naming conventions and ITCSS structure sumarized below;
- Think in components, named with 2 words at least (`.screenshot-image`);
- Components have elements, named with 1 word (`.blog-post > .title`);
- For elements that need two or more words, concatenate them without dashes or underscores (`.firstname`);
- Avoid tag selectors (`> h3`);
- Components and elements may have variants;
- Name variants with a dash prefix (`.shop-banner.-with-icon`);
- Components can nest;
- Avoid reaching into a nested component from the containing component. Instead, add a variant to the nested component and apply it (http://rscss.io/nested-components.html)
- Remember you can extend to make things simple;
- One component per file;
- Use glob matching (`@import 'components/*';`);
- Avoid over-nesting;
- Always use child selectors `>` when possible, it performs better and avoids bleeding through nested components;
- Avoid positioning properties (position, float, margin, dimensions);
- Exception: elements that have fixed width/heights, such as avatars and logos;
- Define positioning in parents (http://rscss.io/layouts.html)
- Use helpers to override values very sparingly. Prefix them with underscores and put them in a separate single file.
- Organize css files in layers using ITCSS

```
                         GENERIC

      ----------------------------------------------
       \                 Settings                 /
        \----------------------------------------/
          \               Tools                /
           \----------------------------------/
             \           Generic            /
              \----------------------------/
                \          Base          /
                 \----------------------/
                   \     Objects      /
                    \----------------/
                      \ Components /  
                       \----------/
                         \Trumps/
                          \    /
                            \/

                         SPECIFIC
```

### References

[TFSports CSS Stats Report](http://cssstats.com/stats?url=http%3A%2F%2Fwww.tfsports.com.br&ua=Browser%20Default)  
[Nicolas Gallagher's blog post "About HTML semantics and front-end architecture"](http://nicolasgallagher.com/about-html-semantics-front-end-architecture/)  
[Awesome css repository](https://github.com/sotayamashita/awesome-css)  
[Airbnb css styleguide official website (good practices for formatting)](https://github.com/airbnb/css)  
[Mark Otto's blog post on GitHub's CSS structure](http://markdotto.com/2014/07/23/githubs-css/)

##### Structure

*RSCSS*  
[RSCSS official website](http://rscss.io)  
[RSCSS official repo](https://github.com/rstacruz/rscss)

*ITCSS*  
[Harry Roberts' talk on ITCSS](https://www.youtube.com/watch?v=1OKZOV-iLj4)  
[Harry Roberts' presentation on ITCSS:](https://speakerdeck.com/dafed/managing-css-projects-with-itcss)  
[ITCSS on twitter](https://twitter.com/itcss_io)  
[Willian Justen's blog post on ITCSS](https://willianjusten.com.br/organizando-seu-css-com-itcss/)  
[James Basoo's blog post on "Scalable, Modular CSS | BEM & ITCSS"](http://www.gpmd.co.uk/blog/scalable-css/)

##### Naming conventions & Methodologies
*BEM*  
[BEM](https://en.bem.info)  
[Harry Roberts' blog post "MindBEMding – getting your head ’round BEM syntax"](https://csswizardry.com/2013/01/mindbemding-getting-your-head-round-bem-syntax/)  
