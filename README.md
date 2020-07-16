# Snooze Eatery Re-Build Estimate Guide

**Table of Contents**
* [Global Theme Setup](#global-theme-setup)
* [ACF Modules](#acf-modules)
	* [Parent ACF Modules](#parent-acf-modules)
	* [Child ACF Modules](#child-acf-modules)
	* [Whole Page Modules](#whole-page-modules)
	* [Possibly Depricated Modules after rebuild](#possibly-depricated-modules-after-rebuild)
* [Custom Post Types](#custom-post-types)
* [Third Party Integrations](#third-party-integrations)
	* [Trabon](#trabon-options)
* [Plugins Audit](#plugins-audit)
	* [Currently Active](#currently-active)
	* [Currently Inactive](#currently-inactive)
* [Page Audit](#page-audit)

## Global Theme Setup:
Things we deemed worthy enough to note which would be important during a site rebuild of Snooze Eatery's WordPress theme.

1) **Theme Style Guide** - Start of an `scss` style guide related to re-usable components throughout the site. These include colors, font faces, button styles, etc.

2) **Site Header** - Site header has a default color for SVG based logo with default value for the full header width. These value can be overwritten on any page via the "Header" field group which gets loaded in the basic page template. These custom fields include:
	* Header Style
		* Original
		* Light
		* Dark
	* Header Width
		* Default 37%
		* Value Range: 0% - 100%

3) **Global Social Media Icons**
	* ACF fields in Global "Theme Options" with the following social media support
		* Facebook
		* Instagram
		* Twitter
		* LinkedIn
		* Email

	**Note:** Icons are reusable SVG's so we can change the background color depending on where they are getting rendered in the markup. Only required SVG fields are 'Social Media Type' and 'Social Media Link'.  

4) **Menus**
	* Header Menu - Menu at the top of the full website.
	* Main Menu - Slide out site nav
		* Main Nav Links
		* 4 Featured Links (From Theme Options)
		* Social Media Icons (From Theme Options)

5) **Site Footer** 
	* Copyright
	* Footer Nav Links
	* Social Media Icons (From Theme Options)

6) **Global Site Popup** - Global site popup option which supports the following
	* Title
	* Body
	* CTA Button
		* Supports Link
		* Custom Modal on click
			* Title
			* Body
			* CTA
	* Color picker for text, background, highlight, and border colors

## ACF Modules
We could potentially re-cycle the ACF module architecture by exporting/importing the ACF modules via `.json`. Then we would only be left with hooking up this logic to the front-end modules with new mark-up. In this site there is a concept of **"Parent Modules"**, **"Child Modules"**, and **Whole Page Modules**. **"Parent Modules"** are the modules available to an admin when creating a new page. **"Child Modules"** are sub-modules that are the building blocks for **"Parent Modules"** which are used to build their internal content. **"Whole Page Modules"** are modules which are loaded into their own page and are not intened to be used with other modules. Although, this theme does not prevent you from doing so, we just assume this based off of their current usage. We could potentially turn these **"Whole Page Moduels"** into their own **"Page Templates"**.

[Module Guide on Staging](#http://staging.tasteful-sugar.flywheelsites.com/module-guide/) - Is a page on the Staging site with example usage for each of the following moduels.

### Parent ACF Modules

1) **[Approved Food](http://staging.tasteful-sugar.flywheelsites.com/module-guide/#approved-food-module)** - Road map module with fixed SVG graphic. Module requires 6 entries, one for each circle in the svg graphic, to complete the map otherwise the module breaks. Note that there is no validation of this requirement, so this module is easy to break of you don't know it's usage. Also has some responsive issues.

2) **[Barista Series](http://staging.tasteful-sugar.flywheelsites.com/module-guide/#barista-series-module)** - Houses two rows of content each containing one media module and one basic content module. Two rows are required maximum/minimum. Front-end slides slides content left to right to reveal row content.
	* Sub-modules
		* Basic Content Module
		* Media Module

3) **[Basic Content](http://staging.tasteful-sugar.flywheelsites.com/module-guide/#basic-content-module)** - This is a "Parent Module", but it is also used a lot as a "Child Module".
	* Supported ACF Fields
		* Content Tab
			* "Show Snooze Font" - boolean to show "Snooze Style Title Group" field group below
			* Snooze Style Title Group - ACF "Snooze Font field group" Sub Modue
			* Content - Full wysiwyg editor
		* Colors Tab
			* Background Color - ACF "Theme Color Picker field group" Sub Module
			* Text Color - ACF "Theme Color Picker field group" Sub Module
			* Highlight Color - ACF "Theme Color Picker field group" Sub Module
		* Buttons Tab - ACF "Buttons field group" Sub Module
		* ~~Input Tab~~ -This tab doesn't work, or at least I can not find a functional usage

4) **[Brands](http://staging.tasteful-sugar.flywheelsites.com/module-guide/#brands-logo)** - ACF Image repeater with the option to add brand logos. They span four logos across before breaking into a new row on the front-end.

5) **[Career Benefits](http://staging.tasteful-sugar.flywheelsites.com/module-guide/#career-benefits-module)** - Simple page module which appends Badges (Imange + Label Repeater) after Basic Content Module.
	* Sub-modules
		* Basic Content Module

6) **[Career Roles](http://staging.tasteful-sugar.flywheelsites.com/module-guide/#career-roles-module)** - Basic Content Module Repeater with optional label. Front-end renders basic content with tabs along the bottom to switch inbetween different entries.
	* Sub-modules
		* Basic Content Module

7) **[Compass](http://staging.tasteful-sugar.flywheelsites.com/module-guide/#compass-content-module)** - This is another module that will break if you don't understand it's usage. There is not field validation to ensure that you are using this module properly. "Slider Image" tab is required.
	* Sub-modules
		* Basic Content Module

8) **[CTA Newsletter](http://staging.tasteful-sugar.flywheelsites.com/module-guide/#cta-newsletter-module)** - Page module with Title and Button which just render's the global e-mail sign-up modal on button click.

9) **[Grid](http://staging.tasteful-sugar.flywheelsites.com/module-guide/#grid-module)** - Image repeater which render's images on the front-end in columns of 3. Images are not being contstrained to match eachother, so potenial rendering issues will occure if the images uploaded are not the same ratio!

10) **[Hero](http://staging.tasteful-sugar.flywheelsites.com/module-guide/#hero-cover-video)** - Hero modules are meant to be used as the first module within a page. This module has a need for height contstraints based of of media on large screens. There are no meda ratio constraints, so depending on the hight of the media; this module could look massive on desktop.
	* Sub-modules
		* Flex Content Module
		* Media Module

11) **[Hero Secondary](http://staging.tasteful-sugar.flywheelsites.com/module-guide/#hero-secondary-module)** - Simpler version of the Hero module. We should double check and see if this module has image ratio constraints, which a lot of these modules do not.

12) **[House](http://staging.tasteful-sugar.flywheelsites.com/module-guide/#house-module)** - Content repeater which builds a house graphic on the front-end. Animations in example usage was made with `.gif` files. Grid turns into a carousel slider on mobile.

13) **[Join the Party](http://staging.tasteful-sugar.flywheelsites.com/module-guide/#join-the-party-module)** - This module's purpose is to promote Snooze's Spotify playlist, but I feel like this could be merged into the triple content module if we wanted to. There are possible rendering issues depending on the height of the content. 
	* Sub-modules
		* Basic Content

14) **[Main Slider](http://staging.tasteful-sugar.flywheelsites.com/module-guide/#main-slider-module)** - Mixed content slider that supports an image, "Basic Content", and Portrait content types. There is not ratio restrictions, so there could be a lot of rendering issues depending on the hight of the media/content added.
	* Sub-modules
		* Pure Slider

15) **[Partners](http://staging.tasteful-sugar.flywheelsites.com/module-guide/#partners-module)** - Tabbed content module with image and custom color settings.
	* Sub-modules
		* ACF "Theme Color Picker field group" Sub Module

16) **[Portrait Slider](http://staging.tasteful-sugar.flywheelsites.com/module-guide/#potrait-slider-module)** - Repeater of Slides module.
	* Sub-modules
		* Slides

17) **[Press Grid](http://staging.tasteful-sugar.flywheelsites.com/module-guide/#press-grid-module)** -  Flex Content module repeater which renders content in a 3 column grid on the front end.
	* Sub-modules
		* Flex Content

18) **[Slider](http://staging.tasteful-sugar.flywheelsites.com/module-guide/#slider-module)** - This is a "Slides Module" repeater which is currently a "Parent Module" but there is not example usages of it being utilized as such. At desktop width, this module has no constraints for the image ratios; so images blow up super large taking up the majority of the screen. We should probably disable it via the "Page: Modules" so it can't be rendered alone or fix the image ratio issue for desktop. It does looks good as a "Sub-Module" in the places where it is re-used.
	* Sub-modules
		* Slides

19) **[Timeline](http://staging.tasteful-sugar.flywheelsites.com/module-guide/#timeline-module)** - Horizontal SVG slider module.

20) **[Triple Content](http://staging.tasteful-sugar.flywheelsites.com/module-guide/#triple-content-module)** - Three required rows of "Flex Content" modules.
	* Sub-modules
		* Flex Content

### Child ACF Modules

1) **[Badges](http://staging.tasteful-sugar.flywheelsites.com/module-guide/#career-benefits-module)** - Repeater with image and label. Example parent module is "Career Benefits" module.
	* Supported ACF Fields
		* Repeater
			* Image (image field)
			* Label (text field)

2) **[Buttons](http://staging.tasteful-sugar.flywheelsites.com/module-guide/#basic-content-module)** - Used in A LOT of places to create CTA buttons inside of many different modules. Example parent module is "Basic Content" module.
	* Supported ACF Fields
		* Layouts Tab
			* Direction (radio button field)
			* Size (radio button field)
			* Aligment (radio button field)
		* Buttons Tab
			* Button (flexible content field)
				* Link (link field)
				* Icon (image field)
				* File Download (bool field)
				* File (file uploader field)

3) **Cover Module** - Title, Content, and Button fields with editable colors.
	* Supported ACF Fields
		* Title (image field)
		* Content (text area field)
		* Background Color - Theme Color Picker Module
		* Text Color - Theme color Picker Module
		* Buttons Module

4) **[Flex Content](http://staging.tasteful-sugar.flywheelsites.com/module-guide/#press-grid-module)** - Flexable content editor which supports many different sub-module types. Although, there is a maximum layout of one entry. Example usage in Press Grid Module.
	* Supported ACF Fields
		* Flexible Content
			* Basic Content Module
			* Image (image field)
			* Cover Module
			* Gallery Module
			* Video Module
			* Portrait Module
			* Media Module

5) **[Gallery](http://staging.tasteful-sugar.flywheelsites.com/module-guide/#press-grid-module)** - Pretty simple module which gets cloned in a LOT of different places. Example usage in Press Grid Module which might not have been intentional.
	* Supported ACF Fields
		* Delay - Range field which controls the slider speed in milliseconds.
		* Gallery (gallery field)

6) **[Media](http://staging.tasteful-sugar.flywheelsites.com/module-guide/#barista-series-module)** - Flexible Content field which supports different media type content. Maximum layout limit of one. Example usage in Barista Series module.
	* Supported ACF Fields
		* Media (Flexible Content Field)
			* Image (block)
				* Image (image field)
			* Video (block)
				* Video Module
			* Counter (block)
				* Counter Module
			* Basic Content (block)
				* Basic Content Module

7) **[Portrait](http://staging.tasteful-sugar.flywheelsites.com/module-guide/#potrait-slider-module)** - This is a sub-module that gets used in the Portraits Slider Module amonst other parent modules.
	* Supported ACF Fields
		* Image (image field)
		* Basic Content Module

8) **[Theme Color Picker](http://staging.tasteful-sugar.flywheelsites.com/module-guide/#basic-content-module)** - Color picker which gets cloned into A LOT of different moduels. Example usage in Basic Content Module.
	* Supported ACF Fields
		* Color (Radio Button)

9) **[Video]((http://staging.tasteful-sugar.flywheelsites.com/module-guide/#hero-cover-video))** - This module gets resued in a lot of different modules to handle video capabilities. Example usage in Hero Module.
	* Supported ACF Fields
		* Video Tab
			* Poster (image field)
			* Source Type (radio button field)
			* Video File (file field)
			* Autoplay (bool field)
			* Plays Fullscreen (bool field)
			* Full Screen Source Type (radio button field)
			* Full Screen Video File (file field)
			* Full Screen Video URL (url field)
			* Show Controls (bool field)
			* Mobile Video (bool field)
		* Mobile Tab
			* Mobile Video Source Type (radio field)
			* Mobile Video File (file field)
			* Mobile Video URL (url field)

### Whole Page Modules

1) **[Contact](http://staging.tasteful-sugar.flywheelsites.com/module-guide-contact-full-page-module/)** - This is a module which is meant to be used on it's own page by itself otherwise rendering issues are possible. This module also queries social media icons via global "Theme Options". This could potentially be handled via a custom "Page Template" rather than a module.
	* Sub-modules
		* States Module

2) **[Gift Cards](http://staging.tasteful-sugar.flywheelsites.com/module-guide-gift-cards-full-page-module/)** - This is another module meant to be used on it's own page otherwise rendering issues are possible. This could potentially be handled via a custom "Page Template" rather than a module. "White screen of death" rendering issue occurs if you do not have at least one "Basic Content" module and one "Press Grid" module.
	* Sub-modules
		* Basic Content
		* Grid/Press Grid (Repeater)

3) **[Menu](http://staging.tasteful-sugar.flywheelsites.com/module-guide-menu-full-page-module/)** - This module is meant to be used on it's own page otherwise it will break the full page if used with other modules. This could potentially be handled via a custom "Page Template" rather than a module. Menu data is queried via Trabon API and rendered manually on the front-end. No iframe is used!
	* Sub-modules
		* Basic Content
		* Gallery Module

4) **[Privacy Policy](http://staging.tasteful-sugar.flywheelsites.com/module-guide-privacy-policy-full-page-module/)** - This modules usage lives on it's own page but doesn't really break anything if used with other modules. This could also be handled by a custom "Page Template" so we don't muddy up the "Parent Module"'s namespace. It uses double "Basic Content" modules to create a title which is kind of confusing to me since this could be condensed into one "Basic Content" module.
	* Sub-modules
		* Basic Content

5) **[States](http://staging.tasteful-sugar.flywheelsites.com/locations/)** - This module's usage lives on it's own page but doesn't break anything if used with other modules. This could be handled via a custom "Page Template" to create the "Find My Snooze" page which will just query locations.

6) **[Sub Navigator](http://staging.tasteful-sugar.flywheelsites.com/breakfast-beliefs/)** - In my openion, this should be handled via it's own "Page Template" in order to have more control over the "SlideTo" action based off of the way the ACF fields get organized. For instance, grouping modules into "SlideTo" groups with a nav label. The current logic is too confusing to use.

### Possibly Depricated Modules after rebuild

1) ~~Catering Form~~ - This is litteraly a custom made gravity form which captures and sends data back to Gravity Form's via an api call. After rebuild, Snooze will be able to embed Gravity Forms via any Basic Page Moduel's content text box.

2) ~~Counter~~ - This module doesn't render on the front-end when used as a parent module meaning something might be broken. It is used as a sub-module via the Media Module and using it there creates a White Screen of Death. We could not find working usage for this module.

3) ~~Locations~~ - This module doesn't render anything on the front-end meaning something might be broken. We could not find any working usage for this module.

4) ~~Content Rotation~~ - Gallery ACF field which allows you to upload multiple images doesn't work on the front-end. It might be the case that this is meant to be used as a sub-module and should be removed from the "Parent" modules so it won't be selectable via "Page: Modules" repeater.

## Custom Post Types

### Branch

* Shows if the post type is equal to the custom post type “Branch”
* Information takes a third of the page, and image rotation takes up the rest of the viewport
* Includes:
	* arrow link that is labeled “Back to all locations” (text input in ACF for label)
	* Name (text) for name of branch
	* General manager field (text)
	* Head chef field (text)
	* Address field (link)
	* Hours field (text)
	* Phone description field (text)
	* Branch gallery (clone of Gallery field group)
	* Branch info (wysiwyg)
	* Delivery and Carryout (text area)
	* Phone number (text)
	* Preview image (image) – displays on state’s page
	* Form Data (group)
		* Label (text)
		* Email (email)
		* Show in After-Hours form (true/false)
		* Show in catering form (true/false)
	* Buttons (clone of Buttons field group)
	* Coordinates (group)
		* Latitude (text)
		* Longitude (text)

### Branches

Repeater with a page link that links to a specific branch 

### Cover 

* Might not be being used often, has “Title” field but it is an image
* Contains:
	* Title (image)
	* Content (text area)
	* Background color (clone of Background color field)
	* Text color (clone of text color)
	* Buttons (clone of Button field group)

### CTA Input

Contains a placeholder (text) and an icon (image)

### Location

* Page/option that details the Location custom post type
* Contains fields:
	* Coming soon (text)
	* Name (text)
	* Image (image)
	* Background color (clone of Theme Color Picker field group)
	* Hide link (true/false)
	* Areas (repeater)
* Name (text)
* Branches (relationship)

### Pure Slider

A slider with an anchor tag and a slides flexible content field that contains a spot for an image, basic content, and a portrait option

### Snoze Font

* This is the font option that can be found many places throughout the site, but can mote notably found in the top of the basic content module to create a stylized title and position it
	* Contains three tabs: content, styles, and color
	* Content contains the text option for content
	* Styles contains:
		* Size (radio button, required)
		* Alignment (radio button, required)
		* Secondary (true/false, changes color fill style of font)
	* Colors contains
		* Fill color (clone of Theme color picker field group)
		* Shadow color (clone of Theme Color picker field group)


### Modules Page

Labeled as “Page: Modules” and consists of all the layouts of the Parent modules

### SEO

Contains a title (text), description (text area), and image (image) field for SEO purposes

## Third Party Integrations

### Trabon Options
This 3rd party is used to query menu data from an API in order to build the "Menu" whole page module.

## Plugins Audit

### Currently Active
* ACF Content Analysis for Yoast SEO
* ~~ACF to WP API~~
* Advanced Custom Fields PRO
* Classic Editor
* CoSchedule
* Custom Fonts
* Duplicate Page
* Gravity Forms
* ~~Header Footer Code Manager~~
* Intuitive Custom Post Order
* Optimize Database after Deleting Revisions
* PNG to JPG
* Regenerate Thumbnails
* Safe SVG
* Webcraftic Robin image optimizer
* WordPress Importer	
* WP Add Custom CSS
* WP Migrate DB Pro
* WP Migrate DB Pro Media Files	
* WP Migrate DB Pro Theme & Plugin Files
* ~~WP REST API~~
* ~~WP REST API Menus~~
* Yoast SEO Premium
* Yoast SEO: Local

### Currently Inactive
* ~~Akismet Anti-Spam~~
* ~~File Renaming on upload~~
* ~~Hello Dolly~~
* ~~WP Migrate DB~~

## Page Audit
This list of pages and modules was taken from the production site on Monday (7/13), for a more accurate representation of the modules being used.

* **4th of July Meal Kits**
	* Basic Content
	* Utilizing custom CSS
* **After Hours** 
	* Catering Form
* **Breakfast Beliefs**
	* Sub Navigator
	* Hero
	* Compass
	* Hero
	* Basic Content
	* Timeline
	* Hero
	* Grid
	* House
* **Careers**     
	* Hero
	* Basic Content
	* Portrait Slider
	* Career Roles
	* Career Benefits
	* Hero
	* Basic Content
* **Catering**
	* Hero
	* Hero
* **Catering Form**
	* Catering Form
* **Contact**
	* Contact
* **Contest Rules**
	* Basic Content
* **COVID-19**
	* Basic Content
* **Drink Menu**
	* Menu
* **Earth Day – DEAD LINK**
	* Basic Content
	* Basic Content
* **Easter Meal Kits – DEAD LINK**
	* Basic Content
	* Basic Content
* **Father’s Day Meal Kits – DEAD LINK**
	* Basic Content
* **Find My Snooze**
	* Hero Secondary
	* States
* **Food Menu**
	* Menu
* **Gift Cards**
	* Gift Cards
* **Make a Weekday Reservation – DEAD LINK**
	* Hero
* **Meal Kit Recipes**
	* Basic Content
* **Mother’s Day Meal Kits – DEAD LINK**
	* Basic Content
* **PPP Loan – Draft**
	* Basic Content
	* Basic Content
* **Press**
	* Hero Secondary
	* Press Grid
* **Privacy Policy**
	* Privacy Policy
* **Restaurant Event Submission**
	* Hero
	* Catering Form
* **Schwag – Draft** 
	* Basic Content
* **Snooze Approved Food**
	* Hero
	* Approved Food
	* Basic Content
	* Partners
	* Brands
	* Basic Content
* **Snooze Neighborhood Provisions**
	* Basic Content
	* Basic Content
	* Basic Content
	* Basic Content
* **Subscribe**
	* Basic Content
* **Weekend Brunch Party**
	* Basic Content
	* Basic Content
* **Breakfast & Brunch Food Restaurant – HOME PAGE**
	* Utilizing Popup
	* Hero
	* Hero
	* Triple Content
	* Triple Content
	* Triple Content
	* Join the Party
	* Barista Series
	* Basic Content
	* Main Slider
	* Basic Content
	* CTA Newsletter
