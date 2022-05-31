---
title: Accessibility
tags: learning
---
# Accessibility

## Accessible React Forms

- https://www.carlrippon.com/accessible-react-forms/

### Inputs and labelling

Bad, label is not associated with checkbox.

Screen readers won't know how to describe it. Clicking the label does nothing.

<label>
  Agree
</label>
<input id="checkbox1" type="checkbox" />

Better; label applies to checkbox.

Screen readers will know how to describe it. Clicking the label toggles the checkbox.

<label for="checkbox2">
  Agree
</label>
<input id="checkbox2" type="checkbox" />

Simple - no need for the "for" attribute, the label wraps the checkbox.

Does change the order they appear in though.

<label>
  <input id="checkbox3" type="checkbox" />
  Agree
</label>

Can also use `aria-labelledby` if you must use a non-label element to label something.

<div id="checkbox-label">Agree</div>
<input type="checkbox" aria-labelledby="checkbox-label" />

Use `aria-describedby` when there is some extra information associated with an input. e.g. Password might be labelled "Password" but have another element nearby describing it as "Passwords must be at least 8 characters long."

The `autocomplete` attribute can be used to speed up data entry, by telling the browser whether a field expects a "name", "email", "street-address" etc.

Required fields on a form can be marked visually with an asterisk, but we should stop screen readers reading it out with `aria-hidden="true"`. Use `aria-required="true"` on the input itself so the screen reader will let the user know.

Use `aria-invalid` to let a user know the data they have entered is not valid.

## Color Contrast

There is a feature in the styles tab of Chrome dev tools that lets you check the color contrast of your text. It also lets you browse palettes to try alternatives in place.

## Visible focus indicators

The default browser focus color may not be high contrast with the rest of your design. It's worth testing this and adjusting if necessary.

If you only want the focus to be visible when someone is navigating with keyboard, use the pseudo-selector `focus-visible` instead of the broader `focus` which applies to mouse clicks too.
