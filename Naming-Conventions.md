We adhere to several naming conventions for both files and elements in the code. This helps ensure consistency and predictability with the use of Clarity.

## General guidelines

* Prefer full words over abbreviations
* Anything public and meant to be used by developers should have the `clr` prefix.

### SCSS & HTML
* Naming conventions - How do we name scss variables and component (child component) elements
* Template structure - What is our preferred approach to structuring style code and templates (I know we are using something bem-ish but I can't remember the name offhand)

### Typescript
#### Naming conventions
##### Components and directives selector
```
clr-component
[clrDirective]
clr-component-subcomponent
[clrComponentSubdirective]
```
Verbose, but no risk of breaking changes due to conflicts.
Abbreviations ok on components with a long name or with a lot of children and grandchildren.

##### Inputs and outputs

For Angular inputs and outputs, we want every instance to start with the prefix `clr` and have a short but accurate name.

```
[clrInput]
(clrInputChange)
(clrOutput)
```
Less verbose, no risk of conflict between component, the only risk is between directives on the same element that both need an extra input that would be named identically.
One advantage is also to allow us to extract reusable directives in the future without breaking changes (see `[clrLoading]`).

##### Components and Directives classname

The basic format is to provide the prefix `Clr` and then a logical name for the component or directive. If the name contains more than one noun, ensure each word is uppercased.

```
ClrWizard (component)
ClrIfOpen (structural directive)
ClrLoading (directive)
```

> Suffixing means breaking changes for internal refactors when switching from Component to Directive, so we're not doing it. Prefix needed to not pollute autocompletion for our consumers.

##### Providers
```
ClrWizardCoordinatorService
ClrIfOpenService
```
As for any publicly exported class, we need to prefix to avoid polluting autocompletion for our consumers. Suffixing with Service is necessary to avoid conflicts with directives or components that share the same name (see 
`IfOpen` for instance).

##### Modules
```
ClrModule / ClarityModule / ClrTheOneModule ???
ClrWizardModule
ClrFormsModule
```
Prefix is obvious to avoid conflicts, and suffixing with Module is a fair convention to make the intent clear for something that's about as public as it can get for a library.

##### Constants
```
private: SCREAMING_SNAKE_CASE
public: CLR_SCREAMING_SNAKE_CASE
```
Public constants are very rare (if we have any), so they'll be prefixed on a per-case basis. Private constants, on the other side, are all over the project and it would be overkill to prefix them.

##### Enums
```
ClrEnum.SCREAMING_SNAKE_CASE
```
It's public, it needs a Clr prefix. Enum values are SCREAMING_SNAKE_CASE because they are constants.

##### Properties and methods
```
ClrModal.open
ClrWizard.next()
```
[Public VS private](#public-vs-private)
```
private subscription: Subscription;

private _open: boolean;
public get open(): boolean;
public set open(value: boolean);

private _openChange: Subject<boolean>;
public get openChange(): Observable<boolean>;
```
Simple private properties do not need an underscore prefix now that we have Typescript.
Private properties that have a corresponding property with the same name can be prefixed with an underscore for better readability.
```
@ContentChildren(Something) _children: QueryList<Something>
_internalMethodThatNeedsToBePublic()
```
Finally, some properties or methods needs to be public for wiring purposes, but we don't want consumers to play with them. These will stay public but be prefixed with an underscore.

##### Filenames

* Components or directives should be named without a suffix like `datagrid-row.ts`, and be placed in the main module folder like `/datagrid/datagrid-row.ts`.
* Providers, factories, services should be named with a suffix like `wizard-navigation.service.ts`, and be placed inside of a `providers` director of the module folder like `/wizard/providers/wizard-navigation.service.ts`.
* Interfaces TBD
* Utilities TBD