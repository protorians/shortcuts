# @Protorians/Shortcut

## Description
The `Shortcut` class allows you to create and manage keyboard shortcuts, including key sequences, on one or more specific HTML elements.

## Imports
```typescript
import { Shortcut, createShortcut } from "@protorians/shortcuts";
```

## Properties

### `targets: T[]`
List of target HTML elements where shortcuts are active.

### `signal: ISignalStack<IShortcutSignalMap>`
Signal manager to track shortcut-related events.

### `shortcuts: IShortcutSequence[]`
Returns the list of registered shortcuts.

### `focused: boolean`
Indicates if at least one of the target elements has focus.

## Options

### `trigger: IShortcutTrigger`
Callback

### `scope?: ShortcutScope`
Shortcut scope. 
`ShortcutScope.Self` : targeted elements,
`ShortcutScope.Global` : Document scope,
`ShortcutScope.Active` : Focused element scope,

### `focused: boolean`
If target is focused

### `timeout: number`
Duration between keys to form the sequence

### `prevent: boolean`
Use `preventDefault` or not when shortcut is triggered

## Constructor
```typescript
constructor(target?: IUiTarget<T>, options: IShortcutOptions = {} as IShortcutOptions)
```
### Parameters
- `target` *(IUiTarget<T> | undefined)*: HTML element or list of elements where shortcuts should be applied.
- `options` *(IShortcutOptions)*: Configuration options for shortcut management.

### Usage Example
```typescript
const shortcut = new Shortcut<HTMLElement>(document.body, { prevent: true });
```

## Static Methods

### `Shortcut.Ctrl(keys: string): string`
Adds `Control+` at the beginning of a key sequence.

### `Shortcut.Shift(keys: string): string`
Adds `Shift+` at the beginning of a key sequence.

### `Shortcut.Meta(keys: string): string`
Adds `Meta+` at the beginning of a key sequence.

### `Shortcut.Alt(keys: string): string`
Adds `Alt+` at the beginning of a key sequence.

### `Shortcut.Command(keys: string): string`
Adds `Command+` at the beginning of a sequence, based on the operating system (`Meta` for Mac/iOS, `Control` otherwise).

### `Shortcut.Option(keys: string): string`
Adds `Option+` at the beginning of a key sequence.

## Public Methods

### `enable(): this`
Enables shortcut detection.

### `disable(): this`
Disables shortcut detection.

### `resolveScope(target: T, scope: ShortcutScope | undefined): T | HTMLElement | undefined`
Determines the scope of shortcut application based on context.

### `mount(sequence: string[], trigger: IShortcutTrigger): this`
Adds a keyboard shortcut.

### Parameters
- `sequence` *(string[])*: Key sequence to trigger.
- `trigger` *(IShortcutTrigger)*: Function to execute when the shortcut is triggered.

### Usage Example
```typescript
shortcut.mount(["Control", "s"], (event) => {
    console.log("Save triggered");
});
```

### `unmount(keys: string[]): this`
Removes a keyboard shortcut.

### `clear(): this`
Removes all registered shortcuts.

## Utility Function

### `createShortcut<T extends HTMLElement>(keys: string[] | string, features: IShortcutTrigger | IShortcutOptions, target?: IUiTarget<T>): IShortcut<T>`
A function that quickly creates a keyboard shortcut.

### Parameters
- `keys` *(string[] | string)*: Key sequence to detect.
- `features` *(IShortcutTrigger | IShortcutOptions)*: Either a trigger function or an options object.
- `target` *(IUiTarget<T> | undefined)*: Target HTML element.

### Usage Example
```typescript
const shortcut = createShortcut("Control+s", (event) => {
    console.log("Save triggered");
});
```
```typescript
const shortcut = createShortcut("Control+s", {
    focused: true,
    trigger: (event) => {
        console.log('Save triggered', event);
    }
}, '.wrapper');
```



# Protorians ;)
