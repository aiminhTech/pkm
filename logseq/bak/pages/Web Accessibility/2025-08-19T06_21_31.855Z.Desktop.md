parent::  [[Website]], [[ARIA]]

-
- ## Ressources
	- ### Course
		- https://frontendmasters.com/courses/accessibility-v3/
			- Exercise: https://learn-a11y.netlify.app/
- ## Overview
  collapsed:: true
	- ==**Web Accessibility**== means that people with **disabilities** can **use** the Web. That means that they can **perceive**, **understand**, **navigate** and **interact** with the web and they can also **contribute** to the Web
	- ### Type of Disabilities
	  collapsed:: true
		- **Mobility and physical**
			- Have limited movement or can’t use a mouse
			- **Example**: Full keyboard navigation, large clickable areas, voice control support
		- **Cognitive and neurological**
			- People with dyslexia, memory issues, or attention difficulties
			- **Example**: Clear language, consistent layouts, avoiding clutter
		- **Visual**
			- Blind, have low vision, or color blindness
			- **Example**: Screen reader support, high contrast mode, text alternatives for images
		- **Hearing**
			- Deaf or hard of hearing
			- **Example**: Captions and transcripts for videos, visual alerts instead of only sounds
	- ### Assistive technologies
	  collapsed:: true
		- Help people with disabilities use websites and apps
			- **Keyboards** – For people who can’t use a mouse.
			- **Wands or mouth sticks** – Used to press keys or touch screens.
			- **Screen readers** – Software that reads text aloud for blind or low-vision users.
			- **Single-use binary devices** – Like large buttons or switches that send one signal (e.g., “click” or “select”).
	- ### Curb-cut effect
	  collapsed:: true
		- When you make something accessible for a specific group, it often helps *everyone*
		- Foir example captions help deaf users, but also people watching videos in noisy places.
-
- ## Standard and Guidelines
	- ### W3C -  World Wide Web Consortium
	  collapsed:: true
		- https://www.w3.org/
		- The International Standards Organization for the WWW
		- Create the Standards fot HTML, CSS and Accessibility
	- ### WAI - W3C Web Accessibility Initiative
	  collapsed:: true
		- https://www.w3.org/WAI/
		- An Initiative within the W3C focused on Accessibility
		- Author of WCAG
	- ### WCAG - Web Content Accessibility Guidelines
		- https://www.w3.org/WAI/standards-guidelines/wcag/
		- The main international standard for web accessibility.
		- Organized under 4 principles: websites must be **Perceivable, Operable, Understandable, and Robust (POUR)**.
	- ### WAI-ARIA
	  collapsed:: true
		- https://www.w3.org/WAI/standards-guidelines/aria/
		- A set of attributes for HTML that help assistive technologies (like screen readers) understand dynamic or interactive content.
	- ### WebAIM
	  collapsed:: true
		- https://webaim.org/
		- Not an official standards body
		- An **independent** advocacy and traning group
		- Provides easy to understand recommendations for Accessibitily
		-
	-
	- ### Conformance Levels in WCAG
	  collapsed:: true
		- **Level A** – Basic accessibility, minimum requirement.
		- **Level AA** – The recommended standard; meets most legal requirements.
		- **Level AAA** – The highest standard; often too strict for all content but ideal where possible.
		- **General rule:** Aim for **WCAG 2.x AA compliance** to stay legally safe and ensure a good experience for most users.
	- ### WCAG POUR principle
	  collapsed:: true
		- Are the foundation of web accessibility. They ensure content is usable by everyone
		- ![image.png](../assets/image_1755244813418_0.png)
-
- ## Assistive Devices
	- ### Screen Readers & Alternative Text
		- Are tools taht convert digital text into spoken words so users can hear what's on the screen. They also let users **navigate using the keyboard** instead of a mouse
		- **Alt text** is essential because images without it make the content meaningless for screen reader users
		- Screen readers will:
			- Read the **alt text** if provided
			- Skip the image if the alt text is empty (for decorative images)
			- Otherwise, they might read the full image URL, which is confusing
- ## Semantic HTML
	- Use elements that **==describe their meaning==** rather than just appearance
	- Examples: `<header>`, `<nav>`, `<main>`, `<button>`, `<form>`
	- **Why?**
		- **Built-in accessibility**: Assistive technologies (like screen readers) **understand semantic elements automatically**
		- **Predictable behavior**: Users can navigate the site more easily
		- **Saves developer time**: Less need for extra ARIA attributes or hacks
	- ### Div Soup
		- Happens when developers use too many `<div>` or `<span>` elements instead of **semantic HTML** like `<button>`, `<header>`, or `<nav>`
		- `<div>` and `<span>` have **no built-in meaning**, so assistive technologies don’t know what they do.
		- To make a `<div>` act like a button, you’d need to add multiple attributes and behaviors manually, like:
			- `role="button"`
			- `tabindex="0"` to make it focusable
			- Keyboard event handlers (Enter/Space)
		- **Better approach:**
			- Use **semantic elements** whenever possible. They come with **built-in accessibility**, saving time and reducing errors.
-
- ## Managing Focus & Tab Order
	-