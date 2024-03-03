What do we absolutely need? I am talking about the bare minimum, but powerful functionality we need for a select component.

Inspiration:

- Radix UI
- Kobalte UI
- Melt UI
- Ariakit

What do they all have in common? How do people use them? What are the most important features?

# Select Research

## Native Select Pain Points:

- Styling is a pain
- Multiselect is not intuitive (especially for non-technical users) It requires ctrl or command keys to select multiple options
- Limited typehead support
- Inconsistent behavior across browsers and devices (including styling)
  re: https://www.custarddoughnuts.co.uk/article/2019/11/3/it-shouldnt-still-be-difficult-to-style-a-select-element

## UX Pain Points:

- Because it's compact, visually indicates it's unimportant
- More difficult to use than a text input
- Users sometimes do not see them
- They look "filled" (the placeholder) even though you need a user input
- Lack of context (confusion on what the purpose of the select is)
- Options are not always visible at once (especially compared to radio buttons)

## When should we use a select?

- Limited space
- Input is nonessential (ex: list sorting)

resource: https://joshwayne.com/posts/the-problem-with-dropdowns/

## Anatomy:

    <Select>
        <SelectTrigger>
            <SelectValue>
        </SelectTrigger>
        <SelectPopover>
            <SelectListbox>
                <SelectOption />
                <SelectGroup label="">
                    <SelectOption />
                </SelectGroup>
            </SelectListbox>
        </SelectPopover>
    </Select>

## Features:

    - [x] Single Select
    - [x] Single Select Keyboard Interactions
    - [ ] Multi Select
    - [ ] Multi Select Keyboard Interactions
    - [x] Controlled or uncontrolled
    - [x] Grouped options
    - [x] Typeahead support (user typing / filter)
    - [x] Looping
    - [ ] RTL support
    - [x] Scrollable
    - [x] Aria (controls, roles, etc)

## Props:

    ### State

    name: value
    type: string
    description: uncontrolled select value

    name: bind:value
    type: Signal
    description: controlled selected value, manages the selected option.

    name: onChange$
    type: PropFunction
    description: function called when the selected value changes.

    name: onOpenChange$
    type: PropFunction
    description: function called when the listbox opens or closes.

    ---

    ### Behavior

    name: placeholder
    type: string
    description: sets a placeholder instead of a selected value.

    name: disabled
    type: boolean
    description: When true, the option is disabled.

    name: multiple
    type: boolean
    description: used for multi-select

    name: loop
    type: boolean
    description: Determines if focus cycles from the last option back to the first, or vice versa.

    ---

    ### Forms

    name: name
    type: string
    description: The name attribute identifies the select element when submitting the form.

    name: required
    type: boolean
    description: When true, the user must select a value to submit the form.

## Keyboard Interactions:

    key: Space
    description: Pressing space opens the select menu and highlights the chosen option. If an option is highlighted, pressing space selects it.

    key: Enter
    description: Pressing Enter opens the select menu and highlights the selected option. If an option is highlighted, pressing Enter selects it.

    key: ArrowDown
    description: Pressing ArrowDown opens the select menu if it's closed. If an option is focused, it moves the focus to the next option.

    key: ArrowUp
    description: Pressing ArrowUp opens the select menu if it's closed. If an option is focused, it moves the focus to the previous option.

    key: Escape
    description: Pressing Escape closes the select menu. The trigger is then focused.

Downsides of our inline component approach:

Much like the native select's drawback, we have a "fixed structure", an expected DOM hierarchy that limits customization. It also throws an error if that hierarchy is not followed.