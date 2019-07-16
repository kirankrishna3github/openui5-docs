| loio |
| -----|
| 497c27a8ee26426faacd2b8a1751794a |

<div id="loio">

view on: [help.sap.com](https://help.sap.com/viewer/DRAFT/3237636b137e43519a20ad5513c49ccb/latest/en-US/497c27a8ee26426faacd2b8a1751794a.html) | [demo kit nightly build](https://openui5nightly.hana.ondemand.com/#/topic/497c27a8ee26426faacd2b8a1751794a) | [demo kit latest release](https://openui5.hana.ondemand.com/#/topic/497c27a8ee26426faacd2b8a1751794a)</div>
<!-- loio497c27a8ee26426faacd2b8a1751794a -->

## Theming

OpenUI5 is an HTML UI library, therefore styling is done using Cascading Style Sheets \(CSS\). This allows for creating an impressive visual experience using a widely known standard technology which is well-accepted on the market.

 OpenUI5 supports you when creating and using different visual designs - called **themes** - that can be used alternatively and switched on the fly. This way, the same application can look very different, depending on the user's design preference or accessibility requirements. Existing themes can serve as a basis for new themes and, in case of new design trends, it is possible to create a matching theme for all existing applications without modifying the applications. The theme handling is decoupled from application development and done in a separate layer. The OpenUI5 library loads the required CSS files and offers ways of switching themes.

On top of pure CSS, OpenUI5 offers a variety of optional features that add value regarding modularization, modification, compatibility, and performance:

-   CSS variables, mixins, color calculations and other functions, provided by the Open Source library [LESS](http://lesscss.org/)
-   In particular, CSS variables are used for centrally defined and centrally modifiable colors
-   Compilation of one CSS file per control library from modular per-control CSS files
-   Optimization/compression of CSS size
-   Clean browser switch and mobile platform detection available \(inside CSS code\)
-   Base theme \(as a basis for a style that is always required to reduce the amount of CSS required for specific themes\)
-   Generic right-to-left support

To ensure these functions, OpenUI5 uses the following components:

-   A CSS generator with several functions: LESS processing \(CSS variables substitution etc.\), merge of CSS files created for different themes and controls for optimal runtime consumption, as well as compression or right-to-left substitution if required.
-   The OpenUI5 runtime handles the loading of the appropriate CSS file for the control libraries used in the application page by adding `<style>` tags to the document head. There is also an API available for switching themes, which replaces the CSS URLs and therefore does not modify the application state.

***

### How to Theme Your OpenUI5 Application

To theme your application, you can choose among a number of options:

-   Adapt an existing theme by using the UI theme designer, which basically modifies the color scheme, but in a very easy, non-technical manner with instant live preview. Adaptation parameters are limited, but the UI theme designer also lets you add custom CSS, which gives you the freedom to adapt basically everything.
-   Create a new theme from scratch, writing every piece of CSS which will then be loaded later. The only requirement is to have `library.css` files within a certain folder structure \(which also defines the theme name\).
-   Adapt an existing theme by adding CSS on application level. This is the easiest option and still sufficient for many use cases. You can technically adapt and change everything. The adaptation is rather done on top of an existing theme and only available within the specific application.

All options except the last one result in a new stand-alone theme which needs to be deployed and referenced by its name in the application and which can be used by any application.

For all these options, the CSS developer might reduce the styling effort and focus on those controls which are actually used in the application \(which in turn decreases the reuse value of the theme in other applications\).

***

### Developing Custom HTML or Your Own Control – What to Bear in Mind

-   To ensure that your OpenUI5 application's OpenUI5 theme can be adapted easily, you should follow some recommendations.

    For more information, see [Creating Themable User Interfaces](CreatingThemableUser_Interfaces_a2c67ac.md).

-   To ensure that your custom content fits the colors of the OpenUI5 theme used, you can use specific CSS classes.

    For more information, see [CSS Classes for Theme Parameters](CSS_Classes_for_Theme_Parameters_ea08f53.md).


***

### More Information

[UI Theme Designer](http://help.hana.ondemand.com/theme_designer/frameset.htm)
