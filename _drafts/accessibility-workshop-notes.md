# Accessibility Workshop Notes

Speaker: Manuel Matuzović at Smashing Conference

Some of his work:

- https://www.matuzo.at/
- https://www.htmhell.dev/
- https://webclerks.at/
- https://www.frontendbookmarks.com/
- https://www.buttoncheatsheet.com/
  - https://marcysutton.com/talk/smashing-conf-sf-the-links-vs-buttons-showdown

Other experts he recommends learning from:

- https://marcysutton.com/
- https://cariefisher.com/

## Intro

Learning how to write HTML well is a key skill.

Accessibility should be considered right from the beginning to get the best results. Building a thing then testing it and hoping to bolt accessibility on at the end will not get the best results.

- Testing
  - Automated with various tools.
    - Nearly all home pages have detectable WCAG 2 failures (97.4% of those tested in WebAIM Million).
  - Manual with devices that our users use, not our favourite set-up!
  - Who? Need to understand who wants to use our website and how they access it.
    - Commonly considered:
      - Mouse
      - Touch
    - Rarely considered:
      - The rest!

- Users
  - Impairment
    - Situational: e.g. my mouse has run out of battery, I'm holding a baby in one arm
    - Temporary: a broken arm stops me using the mouse until it heals
    - Permanent: a motor disability
  - Keyboard
    - Useful for all, _essential_ for some
  - Switch device
    - Typically small number of large buttons.
    - Very versatile - can put a big button anywhere to meet a variety of needs, e.g. on the armrest or headrest of a chair
    - Can assign volume keys of your phone to be switch keys for testing.
    - Modes
      - Scanning (auto, row, group... manual)
        - Move around
        - Automatically gives you a Menu at the top of the UI
      - Enter
        - Select what you have scanned to
      - Point Scan
        - Home in on a particular y then x coordinate and simulate a mouse click there. Allows you to click something that might not be interactive otherwise.
  - Text-to-speech e.g. Screen Reader
    - Blind, dyslexic, difficulty reading, like to multi-task...
    - Side-benefit, if you do this well, it improves your SEO by making it easier for search engines to index your site!
  - Braille display
    - Refreshable displays of Braille - little pips on each cell that pop in and out according to what letter they're showing at the time.
    - Often used by people who are both deaf and blind, but can also just be a preference. Some people use both simultaneously.
  - Voice recognition
    - An alternative to keyboard input; essential for some, useful for all!
    - e.g. Dragon Naturally Speaking (marketed as productivity tool) includes controls as well as text input
  - Zoom / magnification
    - Users should be able to read all content at 2x, 3x, 4x size.
  - Sip and Puff Device
    - A joystick that you can move, sip, and puff to use the three main mouse controls (move, left-click, right-click).

### Keyboard / Switch user: Issues Faced

- Can't focus a button if it's actually a `<div>`
- Missing / hard to see focus styles. Need to know where I am!
- Bad semantics
- Missing key event handlers
- Bad focus management
- Redundant links
  - e.g. Product cards - the whole thing should be clickable. If you wrap every sub-component in links to achieve this you make people tab through N times as many links! The whole thing should be one big link
- Missing skip links (have to tab through loads more than necessary to get to what they want)

### Screen reader user: Issues Faced

- No alternative for multimedia content (video, audio, images)
- Elements with icons only, no text or label
- Incorrect ARIA roles
- Poorly structured content making it hard to get around
  - Not enough structure or too much!
- Overly verbose content
- Overly verbose alt text
- Key events and focus management are important here too!
- Missing feedback or announcements. Have to let people know about changes.

### Voice Recognition: Issues Faced

- No visual label on buttons / controls
- Visible label doesn't match accessible name "Press Go button" won't work if the button is actually called "Search" under the hood.
- Too many labels with same name.
- Small target sizes (oh hey this affects all users!)

### Zoom: Issues faced

- Hard to reach content e.g. tooltips. When you move the mouse to read it, the tooltip disappears!
- Hard to read content. e.g. If line-height doesn't grow with text size it will end up overlapping when you zoom in.
- Overflow - horizontal scrolling isn't a major issue but it's annoying.
- Cut-off content.

We have a large range of user needs and technologies to consider there. This so far has been focussed on input and output modes, we can also consider color contrast, animation, content strategy, cognitive needs etc.

### Stats!

WebAIM conduct surveys - e.g. asking screen readers what their most common problems navigating websites are.

Also can search for people telling their own stories, e.g. Holly Tuke's blog about most annoying things encountered in her use of the web.

### Lang attribute

Sits on the `<html>` tag.

Tells browser tools like Google Translate what language the content is in so it knows how to read it.

Also facilitates some stylistic things like languages typesetting quote marks differently.

Tells screen readers how to pronounce words.

## Automated Accessibility Testing

There are many tools! They allow us to catch the easy fixes quickly.

### Lighthouse

Built into Google Chrome, Node, CLI, CI and a web version available.

It's error messages link to documentation - making it good for learning as well as testing.

As well as fails, it tells you about things you passed on - you can learn about what you're doing well, even if you didn't realise you were doing it well.

It's powered by the "Axe" engine, which is widely used in automated accessibility testing.

#### The Accessibility Tree

You write HTML. The browser turns that into the DOM. The other representation of your document is called the Accessibility Tree. It includes all the accessible elements of your page, their labels and the states they're in. If you `aria-hidden` an element, it's not in this tree. So focusable elements shouldn't be `aria-hidden` or they'll be tab-focusable with no way to know what they are.

---

## Further Reading

- WAI
- WebAIM, e.g. surveys
- WCAG
- ARIA: Accessible rich internet applications
- A11yCasts playlist
- Christopher Hills on YouTube (switch user)
- web.dev how to do an accessibility review - https://web.dev/how-to-review/
