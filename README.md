# Layouts || UX 2018

A personal collection of projects, demos and online course work revisiting layout fundamentals and best practices in 2018 with the goal of exploring the latest techniques and testing strategies to ensure that designs are:

* Accessible
* Maintainable
* Inclusive
* Beautiful

Web layout is generally concered with how components align and flow in the context of the page and viewport. But components themselves are often containers of other components, aware only of their own parent containers. Because of this fractal nature, it's never a good idea to design layouts in isolation of other UI concerns. It wireframe or mockup first approach is attractive, addressing the needs of the app from a purely aesthetic point of view. However, this leads to box thinking as well as a lot of repeated effort, miscommunication, and mismanagement of expectations between stakeholders.

Design the application, not a screenshot of the application. On the other end of the spectrum, designing a full-scale component or pattern library from the bottom-up without a clear direction for the app as a whole is a good way to do a lot of extra work without getting much closer to the stated goal of creating an app.

Layout is a good starting place for UI design; it gives us neat slots to fill in. But it needs to be rooted in a few good principles. From the outset, a good design should address the functional needs of both the end-user and the codebase user. It should envision a multifaceted interface that's a joy to work with and a joy to use. Disorganized and inflexible systems are only a joy to discard.

Consideration for a wide range of users and devices, for naming and categorical conventions, codebase maintainability, and aesthetic beauty should all be undertaken with the first round of laying out the application. Ideally, this undertaking produces a working prototype, a real, interactive static application (perhaps with basic routing) like a shell or foundation for further development, not a bait-and-switch for signoff. First round deliverables should be readable, flexible, modular, well-tested, well-documented, and ready to hand off and plug in to other systems for enhanced functionality.

Starting with a pre-written component library like Bootstrap may address some of these concerns. These tools are great for projects where branding will never be a priority. However, when choosing this route, there's a good chance that at some point during the application's lifespan, more time will have been spent customizing the library than if it had been built from scratch. More likely, though, leaning on this tool will lead to bypassing the design process entirely, failing to ask some of the most important existential questions about app at a crucial stage of inception, putting these off to a later date when the inclination is to either scrap it or rebuild from scratch.

## Notes

### Accessibility

* Refer to the [WebAIM checklist](https://webaim.org/standards/wcag/checklist)
* Provide keyboard shortcuts for UI
* Only certain elements are tabbable:

```
'a[href], area[href], input:not([disabled]), select:not([disabled]), textarea:not([disabled]), button:not([disabled]), iframe, object, embed, [tabindex="0"], [contenteditable], audio[controls], video[controls]'
```

* You can use the `tabindex` attribute to make a non-tabbable element tabbable, override default order, or to skip a tabbable element
* Style `:focus` state for visible focus
* Add a skip link at the top of the document to allow users to skip to the main content
* Focus control with `document.activeElement`; you can capture this value when a user enters a modal and then call `.focus()` on it when they close
* Tabtrapping: get a list of all tabable elements inside a modal, listen for the shift and tab keys, and `preventDefault()` and manually set the next tabbed element with `.focus()` when a user reaches the last item going forwards or the first element going backwards.
* Screen Readers: (use `⌘ + F5` in OSX, try ZoomText in OSX, JAWS in Windows, ChromeVox in the Browser)
* Alt text: empty gets skipped, UPPERCASE gets read letter-by-letter
* Use an alt attribute with an empty value to skip images not for screen readers
* Screen readers don't read `display:none`, `visibility:hidden`, `[hidden]`
* For screen readers but not other users, absolute position outside of the viewport or use `background-clip`
* Labels are important for screenreaders; it's fine to visually hide them
* Alternatively, you can set a value to `aria-labelledby` on the form elements themselves
* Use `role` attribute
* Avoid using captchas if possible
* Semantics: always define the language in the html `lang` attribute
* Semantics: use real `button` and `input[type=checkbox]` elements
* Semantics: use appropriate headings; use CSS to override size and style defaults
* Use `aria-describedby` to provide a lengthier description of the UI feature. You can set it to the id of another element with the helper text.
* Use aria properties in CSS attribute selectors, e.g. [aria-expanded="false"]
* Use the `aria-live` attribute on a region of the site that demands attention and is going to be updating.
* Use the `aria-relevant` attribute for specific updates that should be highlighted to the user

#### Tools

* Visual Impairment: NoCoffee Visual Simulator extension
* Analyze color palettes: [Create a Color Palette Accessibility Evaluator
  ](https://accessibility.oit.ncsu.edu/tools/color-contrast/index.php?colors=ffffff,f5f5f5,d5d5d5,e5e5e5,333333,666666,e5f7ff,00628c,00354C,00628,C,008FCC,006e9dmain), [Accessible color palette builder](https://toolness.github.io/accessible-color-matrix/), [Color Safe](http://colorsafe.co/), [Material Color Tool](https://material.io/color/)
* Do not use color as the sole way to communicate or distinguish any content or interface
* Use the accessibility audit in Chrome's built-in [Lighthouse](https://developers.google.com/web/tools/lighthouse/) feature in the console. It can be run from the [command line or as a node module](https://github.com/GoogleChrome/lighthouse). Try to incorporate this tool into the design build process and continuous integration workflow. Also, comes with some other useful audits.
* [Tenon.io](https://tenon.io/) API
* [tota11y](http://khan.github.io/tota11y/), an accessibility visualization toolkit
* [a11y](https://github.com/addyosmani/a11y), command line tool for accessibility audits powered by the Chrome Accessibility Tools
* Testing tools for React: [react-a11y](https://github.com/reactjs/react-a11y); can use it in testing suites:

```
beforeEach(() => a11y(React))
afterEach(() => a11y.restoreAll())
```

* Also, read the [Accessibility section of the react docs](https://reactjs.org/docs/accessibility.html)
* The VueJS community is currently working on a [guide](https://github.com/vuejs/vuejs.org/pull/1002)

Source: [Website Accessibility on FrontendMasters](https://frontendmasters.com/courses/web-accessibility/)

See also: [WebAIM](https://webaim.org/)

### CSS Maintainability

#### SMACSS

SMACSS is a simple approach to structuring modular CSS. It establishes a convention for ordering CSS classes by specificity, dividing them into 5 categories:

1.  **Base Rules**: Element selector rules and resets that apply as always-ok defaults.
2.  **Layout Rules**: Rules specific to the alignment and flow of 'major' components, such as header, main, and footer, distinct from that of 'minor' components.
3.  **Module Rules**: Rules for 'minor' components or the components that are nested in the 'major' components, such as navigation bars, carousels, dialogs, widgets, etc.
4.  **State Rules**:
5.  **Theme Rules**:

Source: [SMACSS site](https://smacss.com/)

#### BEM

[GetBEM.com](http://getbem.com/introduction/)

[ABEM. A more useful adaptation of BEM.](https://css-tricks.com/abem-useful-adaptation-bem/)

#### Component-scoped CSS

[react-css-modules](https://github.com/gajus/react-css-modules)

[VUE Scoped CSS](https://vue-loader.vuejs.org/en/features/scoped-css.html)

### Inclusive

#### Responsive

#### Cross-browser support

#### Performance

#### Internationalization

### Beautiful
